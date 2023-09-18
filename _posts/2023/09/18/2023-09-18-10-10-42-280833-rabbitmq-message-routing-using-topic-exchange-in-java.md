---
layout: post
title: "RabbitMQ message routing using topic exchange in Java"
description: " "
date: 2023-09-18
tags: [rabbitmq, topicexchange]
comments: true
share: true
---

Message routing is a crucial part of building distributed systems. RabbitMQ, a popular message broker, provides various exchange types for routing messages. One of the most flexible exchange types is the topic exchange.

In this blog post, we will explore how to use the topic exchange in RabbitMQ for message routing in Java.

## Prerequisites

Before getting started, make sure you have the following installed:

1. RabbitMQ server
2. Java Development Kit (JDK)
3. RabbitMQ Java client library

## Setting up a Topic Exchange

To create a topic exchange in RabbitMQ, we will use the `TopicExchange` class provided by the RabbitMQ Java client library. Here's an example code snippet to set up a topic exchange:

```java
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import java.io.IOException;

public class TopicExchangeSetup {

    private static final String EXCHANGE_NAME = "my_topic_exchange";

    public static void main(String[] args) {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");

        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {

            // Create a topic exchange named "my_topic_exchange"
            channel.exchangeDeclare(EXCHANGE_NAME, "topic");
            System.out.println("Topic exchange created successfully!");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```
Make sure to replace `localhost` with the actual hostname or IP address of your RabbitMQ server.

## Publishing Messages with Routing Keys

To publish messages with routing keys, we will use the `BasicPublish` method provided by the RabbitMQ Java client library. Each message is published with a specific routing key that matches a pattern specified in the topic exchange.

Here's an example code snippet to publish messages with routing keys:

```java
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import java.io.IOException;
import java.nio.charset.StandardCharsets;

public class MessagePublisher {

    private static final String EXCHANGE_NAME = "my_topic_exchange";

    public static void main(String[] args) {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");

        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {

            String routingKey = "com.myapp.critical";

            // Publish a message with routing key "com.myapp.critical"
            channel.basicPublish(EXCHANGE_NAME, routingKey, null, "Hello, RabbitMQ!".getBytes(StandardCharsets.UTF_8));
            System.out.println("Message published successfully!");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In the above code, we publish a message with the routing key `com.myapp.critical` to the topic exchange.

## Subscribing to Messages with Binding Patterns

To subscribe to messages with specific routing key patterns, we need to bind a queue to the topic exchange with a routing key pattern using the `QueueBind` method.

Here's an example code snippet to subscribe to messages with specific binding patterns:

```java
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.DeliverCallback;
import java.io.IOException;

public class MessageSubscriber {

    private static final String EXCHANGE_NAME = "my_topic_exchange";
    private static final String QUEUE_NAME = "my_topic_queue";

    public static void main(String[] args) {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");

        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {

            channel.queueDeclare(QUEUE_NAME, false, false, false, null);

            String bindingPattern = "*.critical";

            // Bind the queue to the topic exchange with binding pattern "*.critical"
            channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, bindingPattern);

            System.out.println("Waiting for messages...");

            DeliverCallback deliverCallback = (consumerTag, delivery) -> {
                String message = new String(delivery.getBody(), "UTF-8");
                System.out.println("Received message: " + message);
            };

            // Start consuming messages from the queue
            channel.basicConsume(QUEUE_NAME, true, deliverCallback, consumerTag -> {
            });

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In the above code, we bind a queue named `my_topic_queue` to the topic exchange with a binding pattern `*.critical`. This means the queue will only receive messages with routing keys matching the pattern.

## Conclusion

In this blog post, we learned how to use the topic exchange in RabbitMQ to implement message routing in Java. We explored how to set up a topic exchange, publish messages with routing keys, and subscribe to messages with specific binding patterns.

By using the topic exchange, we can build flexible and scalable distributed systems where messages can be selectively routed based on various routing key patterns.

#rabbitmq #topicexchange