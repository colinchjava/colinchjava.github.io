---
layout: post
title: "Implementing a cache with asynchronous loading using CompletableFuture and HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In many applications, caching is an effective technique to improve performance by reducing the load on the database or external services. In this blog post, we will explore how to implement a cache with asynchronous loading capability using the CompletableFuture class and a HashMap in Java.

## Table of Contents
- [Introduction](#introduction)
- [Creating the Cache](#creating-the-cache)
- [Asynchronous Loading](#asynchronous-loading)
- [Using the Cache](#using-the-cache)
- [Conclusion](#conclusion)

## Introduction

The cache we'll implement will contain key-value pairs, where the key is a unique identifier and the value is the data associated with that identifier. The cache will utilize a HashMap to store the data, providing O(1) time complexity for read and write operations.

## Creating the Cache

First, we need to create a class to represent our cache. Let's call it `Cache` and declare it as a generic class with two type parameters: K for the key type and V for the value type.

```java
public class Cache<K, V> {
    private final Map<K, V> cache;

    public Cache() {
        this.cache = new HashMap<>();
    }
    
    // Methods for adding, retrieving, and removing data from the cache
}
```

In this code snippet, we initialize the cache using a HashMap in the constructor.

## Asynchronous Loading

To implement asynchronous loading, we can use the CompletableFuture class introduced in Java 8. CompletableFuture provides a convenient way to perform computations asynchronously and handle the results when they become available.

```java
import java.util.concurrent.CompletableFuture;

public class Cache<K, V> {
    // ...

    public CompletableFuture<V> getAsync(K key) {
        return CompletableFuture.supplyAsync(() -> {
            // Load data if not present in the cache
            if (!cache.containsKey(key)) {
                V value = loadData(key);
                cache.put(key, value);
            }
            return cache.get(key);
        });
    }
    
    private V loadData(K key) {
        // Simulating loading data from a slow data source or external service
        // Replace this with your own implementation
        try {
            Thread.sleep(1000); // Simulate delay of 1 second
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
        // Return the loaded data
        return // ...
    }
}
```

In the code above, we define the `getAsync` method that asynchronously loads the data associated with the given key. If the key is already present in the cache, the method immediately returns the corresponding value. Otherwise, it uses `CompletableFuture.supplyAsync` to perform the data loading task asynchronously.

The `loadData` method simulates loading data from a slow data source or external service by introducing a delay of one second. Replace this method with your own implementation to load the actual data.

## Using the Cache

To use the cache, create an instance of the `Cache` class and call the `getAsync` method to fetch the data asynchronously.

```java
public class Main {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        Cache<String, String> cache = new Cache<>();
        
        CompletableFuture<String> future1 = cache.getAsync("key1");
        CompletableFuture<String> future2 = cache.getAsync("key2");
        
        String value1 = future1.get();
        String value2 = future2.get();
        
        System.out.println(value1);
        System.out.println(value2);
    }
}
```

In this example, we create a cache instance and fetch two values asynchronously using the `getAsync` method. We then obtain the results by calling the `get` method on the CompletableFuture objects. The retrieved values will be printed to the console.

## Conclusion

Implementing a cache with asynchronous loading capability can greatly improve the performance and responsiveness of your applications. By using CompletableFuture and HashMap, we can easily achieve this functionality in Java. Remember to replace the `loadData` method with your own logic to load the actual data.

Implementing such a cache can be beneficial in scenarios where you frequently access slow data sources or external services, reducing latency and improving overall application responsiveness.