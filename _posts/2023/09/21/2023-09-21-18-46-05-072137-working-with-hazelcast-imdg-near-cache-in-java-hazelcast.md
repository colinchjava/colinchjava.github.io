---
layout: post
title: "Working with Hazelcast IMDG near cache in Java Hazelcast"
description: " "
date: 2023-09-21
tags: [HazelcastIMDG, NearCache]
comments: true
share: true
---

Hazelcast IMDG (In-Memory Data Grid) is a distributed computing platform that provides highly scalable storage for data-intensive applications. One of the key features of Hazelcast IMDG is its Near Cache mechanism, which allows for faster access to frequently accessed data.

## What is Near Cache?

Near Cache is an in-memory cache that resides on the client side of a Hazelcast cluster. It stores a copy of the data that is stored in the cluster, allowing for faster data access and reducing the number of network calls.

When a read operation is performed on the Hazelcast cluster, the Near Cache is checked first. If the data is found in the Near Cache, it is returned immediately without any network overhead. If the data is not found, Hazelcast fetches it from the cluster and updates the Near Cache for future use.

## Benefits of Near Cache

Using the Near Cache can provide several benefits:

1. **Improved performance**: Accessing frequently read data directly from the client-side cache eliminates the need for network round trips, resulting in faster response times.

2. **Reduced network overhead**: By serving data from the near cache, you can reduce the overall network traffic between the client and the cluster, which can be especially beneficial in scenarios with high read operations.

3. **Lower latency**: Near Cache allows for lower latency as the data is retrieved locally without the need to traverse the network.

## Configuring Near Cache in Hazelcast IMDG

To configure Near Cache in Hazelcast IMDG, you need to define it in the client configuration. Here's an example of how to configure Near Cache in Java:

```java
Config config = new Config();
NearCacheConfig nearCacheConfig = new NearCacheConfig()
  .setName("myCache")
  .setInMemoryFormat(InMemoryFormat.OBJECT)
  .setTimeToLiveSeconds(60);

config.getMapConfig("myMap")
  .setNearCacheConfig(nearCacheConfig);

HazelcastInstance hazelcastInstance = Hazelcast.newHazelcastInstance(config);
```

In the above example, we define a Near Cache named "myCache" for the map named "myMap". We set the `InMemoryFormat` to `OBJECT` to store the data in serialized form. We also specify the `timeToLiveSeconds` to define the expiration time for the entries in the Near Cache.

## Monitoring Near Cache

Hazelcast IMDG provides several ways to monitor the Near Cache:

1. **Hazelcast Management Center**: The Hazelcast Management Center provides a web-based interface to monitor and manage your Hazelcast cluster. It offers detailed insights into the Near Cache statistics and performance metrics.

2. **Metrics API**: You can use the Hazelcast Metrics API to programmatically retrieve Near Cache statistics and monitor the performance of your cache.

## Conclusion

Hazelcast IMDG Near Cache is a powerful mechanism to accelerate data access in data-intensive applications. By configuring and utilizing the Near Cache, you can significantly improve application performance and reduce network overhead. Experiment with Near Cache in your Hazelcast IMDG setup and experience faster data access firsthand!

#Java #HazelcastIMDG #NearCache