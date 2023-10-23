---
layout: post
title: "Implementing a cache with lazy loading using a custom proxy and HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

Caching is a common technique used in software development to improve the performance of an application. It involves storing frequently accessed data in a cache to reduce the need for expensive or time-consuming operations, such as retrieving data from a database or making remote API calls. In this article, we'll explore how to implement a cache with lazy loading using a custom proxy and HashMap in Java.

## Table of Contents
- [Introduction](#introduction)
- [Lazy Loading](#lazy-loading)
- [Custom Proxy](#custom-proxy)
- [HashMap](#hashmap)
- [Implementation](#implementation)
- [Conclusion](#conclusion)

## Introduction
A cache is essentially a temporary storage that holds data that is expected to be frequently used. It provides faster access to the data, as it eliminates the need to retrieve it from the original source every time. In a lazy loading cache, data is loaded into the cache only when it is requested for the first time.

## Lazy Loading
Lazy loading is a design pattern where the data is loaded into memory only when it is actually needed. This approach helps optimize system resources by loading data on demand rather than loading everything upfront. In our cache implementation, we will utilize lazy loading to fetch data from the original source only when it is requested.

## Custom Proxy
To implement lazy loading, we'll make use of a custom proxy class. A proxy acts as an intermediary between the client code and the actual object being accessed. In our case, the proxy will intercept the calls to the cache and handle the lazy loading of data if it is not already present.

## HashMap
In Java, the HashMap class provides an efficient way to store key-value pairs. We'll use a HashMap to store the cached data, where the keys will correspond to the unique identifiers of the data items, and the values will hold the actual data.

## Implementation
Here's an example implementation of a cache with lazy loading using a custom proxy and HashMap in Java:

```java
import java.util.HashMap;
import java.lang.reflect.InvocationHandler;
import java.lang.reflect.Method;
import java.lang.reflect.Proxy;

public class LazyLoadingCache<K, V> implements InvocationHandler {
    private HashMap<K, V> cache;
    private DataProvider<K, V> dataProvider;

    private LazyLoadingCache(DataProvider<K, V> dataProvider) {
        this.cache = new HashMap<>();
        this.dataProvider = dataProvider;
    }

    @SuppressWarnings("unchecked")
    public static <K, V> V create(DataProvider<K, V> dataProvider) {
        return (V) Proxy.newProxyInstance(
                dataProvider.getClass().getClassLoader(),
                dataProvider.getClass().getInterfaces(),
                new LazyLoadingCache<>(dataProvider)
        );
    }

    @Override
    public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
        if (method.getName().equals("get")) {
            K key = (K) args[0];
            V value = cache.get(key);
            
            if (value == null) {
                value = dataProvider.get(key);
                cache.put(key, value);
            }
            
            return value;
        }
        
        throw new UnsupportedOperationException("Method not supported: " + method.getName());
    }
}
```

In the above implementation, we define a `LazyLoadingCache` class that implements the `InvocationHandler` interface. The `create` method is used to create an instance of the cache object, which is a dynamic proxy that implements the same interface as the data provider.

The `invoke` method is invoked whenever a method is called on the cache object. If the method is `get`, we check if the requested data is present in the cache. If not, we fetch the data from the data provider and store it in the cache before returning the value. If the method is not `get`, we throw an exception as this cache implementation only supports the `get` operation.

To use the cache, you need to provide an implementation of the `DataProvider` interface, which defines a `get` method to retrieve the data based on a given key. Here's how you can create a simple data provider:

```java
public interface DataProvider<K, V> {
    V get(K key);
}
```

You can then use the cache as follows:

```java
DataProvider<String, String> dataProvider = key -> {
    // Retrieve the data from the original source
    // This can be a database query, remote API call, etc.
    return "Data for key: " + key;
};

DataProvider<String, String> cachedDataProvider = LazyLoadingCache.create(dataProvider);

String data1 = cachedDataProvider.get("key1"); // Fetches data from data provider
String data2 = cachedDataProvider.get("key1"); // Retrieves cached data

System.out.println(data1); // Output: Data for key: key1
System.out.println(data2); // Output: Data for key: key1
```

In the above example, the first call to `get("key1")` fetches the data from the data provider, while the second call retrieves the cached data. This demonstrates the lazy loading behavior of the cache.

## Conclusion
Implementing a cache with lazy loading can significantly improve the performance of your application by reducing the need for repetitive and resource-intensive operations. By using a custom proxy and a HashMap, you can easily build a simple and efficient cache that provides lazy loading capabilities.