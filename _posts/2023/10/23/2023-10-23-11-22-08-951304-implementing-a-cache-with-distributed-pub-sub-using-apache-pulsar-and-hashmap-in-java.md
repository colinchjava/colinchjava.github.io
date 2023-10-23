---
layout: post
title: "Implementing a cache with distributed pub-sub using Apache Pulsar and HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

- [Introduction](#introduction)
- [Implementing a Cache with Distributed Pub-Sub](#implementing-a-cache-with-distributed-pub-sub)
- [Setting Up Apache Pulsar](#setting-up-apache-pulsar)
- [Creating a HashMap Cache](#creating-a-hashmap-cache)
- [Publishing and Subscribing to Pulsar Topics](#publishing-and-subscribing-to-pulsar-topics)
- [Putting It All Together](#putting-it-all-together)
- [Conclusion](#conclusion)

## Introduction

In modern distributed systems, caching plays a crucial role in improving performance and reducing latency. Apache Pulsar, a highly scalable messaging system, can be an excellent choice for implementing a cache with distributed pub-sub capabilities. In this article, we will explore how to implement a cache using Apache Pulsar and a HashMap in Java.

## Implementing a Cache with Distributed Pub-Sub

Distributed pub-sub allows multiple instances of a cache to synchronize their data and stay consistent with each other. Apache Pulsar provides a pub-sub messaging model, allowing publishers to send messages to topics and subscribers to receive these messages. By leveraging Pulsar's pub-sub capabilities, we can implement a distributed cache where cache updates are published as messages.

## Setting Up Apache Pulsar

To use Pulsar in our Java project, we need to add the necessary dependencies to our build configuration. We can do this by adding the following Maven dependencies to our `pom.xml` file:

```xml
<dependency>
    <groupId>org.apache.pulsar</groupId>
    <artifactId>pulsar-client</artifactId>
    <version>2.9.2</version>
</dependency>
<dependency>
    <groupId>org.apache.pulsar</groupId>
    <artifactId>pulsar-functions-api-java</artifactId>
    <version>2.9.2</version>
</dependency>
```

Once the dependencies are added, we can proceed with creating the cache implementation.

## Creating a HashMap Cache

In our cache implementation, we will use a `HashMap` to store the key-value pairs. Here's a basic example of creating a cache:

```java
import java.util.HashMap;
import java.util.Map;

public class Cache {
    private Map<String, String> cacheMap;

    public Cache() {
        cacheMap = new HashMap<>();
    }

    public void put(String key, String value) {
        cacheMap.put(key, value);
    }

    public String get(String key) {
        return cacheMap.get(key);
    }

    public void remove(String key) {
        cacheMap.remove(key);
    }
}
```

This is a simple cache implementation using a `HashMap` where we can store and retrieve values based on their keys.

## Publishing and Subscribing to Pulsar Topics

To enable distributed synchronization, we need to publish cache updates as messages to Pulsar topics and subscribe to these topics on all cache instances. Here's an example of how we can publish and subscribe to Pulsar topics:

```java
import org.apache.pulsar.client.api.Consumer;
import org.apache.pulsar.client.api.Producer;
import org.apache.pulsar.client.api.PulsarClient;
import org.apache.pulsar.client.api.PulsarClientException;
import org.apache.pulsar.client.api.Schema;
import org.apache.pulsar.client.api.SubscriptionMode;
import org.apache.pulsar.client.api.SubscriptionType;
import org.apache.pulsar.client.api.TypedMessageBuilder;

public class PulsarPubSub {
    private static final String PULSAR_SERVICE_URL = "pulsar://localhost:6650";
    
    public void publishMessage(String topic, String message) throws PulsarClientException {
        PulsarClient client = PulsarClient.builder()
                .serviceUrl(PULSAR_SERVICE_URL)
                .build();
        
        Producer<String> producer = client.newProducer(Schema.STRING)
                .topic(topic)
                .create();
        
        producer.newMessage()
                .key("cache-update")
                .value(message)
                .send();
        
        producer.close();
        client.close();
    }
    
    public void subscribeToTopic(String topic) throws PulsarClientException {
        PulsarClient client = PulsarClient.builder()
                .serviceUrl(PULSAR_SERVICE_URL)
                .build();
        
        Consumer<String> consumer = client.newConsumer(Schema.STRING)
                .topic(topic)
                .subscriptionType(SubscriptionType.Exclusive)
                .subscriptionMode(SubscriptionMode.Durable)
                .subscriptionName("cache-subscription")
                .subscribe();
        
        while (true) {
            consumer.receiveAsync().thenAcceptAsync(message -> {
                // Handle received message
                processMessage(message.getValue());
            });
        }
    }
    
    private void processMessage(String message) {
        // Update the cache based on the received message
    }
}
```

In this example, we create a Pulsar client and a producer to publish messages to a topic. We also create a consumer to subscribe to the topic and process received messages asynchronously.

## Putting It All Together

To implement the cache with distributed pub-sub, we can combine the `Cache` class with the `PulsarPubSub` class. Whenever a cache update occurs, we publish a message to the Pulsar topic. All cache instances subscribed to the topic will receive the message and update their local cache accordingly.

```java
public class DistributedCache {
    private Cache cache;
    private PulsarPubSub pulsarPubSub;
    private String cacheTopic;

    public DistributedCache(String cacheTopic) {
        this.cache = new Cache();
        this.pulsarPubSub = new PulsarPubSub();
        this.cacheTopic = cacheTopic;
    }

    public void put(String key, String value) {
        cache.put(key, value);
        
        // Publish cache update to Pulsar topic
        pulsarPubSub.publishMessage(cacheTopic, createCacheUpdateMessage(key, value));
    }

    public String get(String key) {
        return cache.get(key);
    }

    public void remove(String key) {
        cache.remove(key);
        
        // Publish cache update to Pulsar topic
        pulsarPubSub.publishMessage(cacheTopic, createCacheRemoveMessage(key));
    }

    private String createCacheUpdateMessage(String key, String value) {
        // Create cache update message format
        return "UPDATE:" + key + "=" + value;
    }

    private String createCacheRemoveMessage(String key) {
        // Create cache remove message format
        return "REMOVE:" + key;
    }

    public void startCacheSync() throws PulsarClientException {
        // Subscribe to Pulsar topic for cache updates
        pulsarPubSub.subscribeToTopic(cacheTopic);
    }
}
```

In this final implementation, whenever a cache operation (put or remove) occurs, we publish the cache update to the Pulsar topic using the `PulsarPubSub` instance. We also start cache synchronization by subscribing to the Pulsar topic in the `startCacheSync` method.

## Conclusion

Implementing a cache with distributed pub-sub using Apache Pulsar and a HashMap in Java can greatly enhance the scalability and consistency of a cache in a distributed system. By leveraging Pulsar's pub-sub capabilities, cache updates can be efficiently propagated across cache instances.