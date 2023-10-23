---
layout: post
title: "Implementing a cache with time-based expiration using a custom scheduler and HashMap in Java"
description: " "
date: 2023-10-23
tags: [caching]
comments: true
share: true
---

Caching is a common technique used in software development to improve performance by storing frequently accessed data in memory. One of the challenges with caching is managing the expiration of cached data to ensure its relevance. In this blog post, we will explore how to implement a cache with time-based expiration using a custom scheduler and HashMap in Java.

## Table of Contents
- [Understanding caching and expiration](#understanding-caching-and-expiration)
- [Implementing the cache](#implementing-the-cache)
- [Using a custom scheduler](#using-a-custom-scheduler)
- [Conclusion](#conclusion)

## Understanding caching and expiration

Caching involves storing the results of expensive operations or frequently accessed data in memory for faster retrieval. However, cached data can become stale over time and lead to incorrect or outdated results. To address this, we need to design a cache implementation that periodically checks the expiration of cached entries and removes them when necessary.

## Implementing the cache

We can use the `HashMap` data structure in Java to implement an in-memory cache. The key-value pairs in the `HashMap` will represent the cached data, where the key is the identifier and the value is the cached data itself. Additionally, we need to store the expiration time along with each cached entry.

```java
import java.util.HashMap;

public class Cache<K, V> {
    private HashMap<K, CacheEntry<V>> cache;

    public Cache() {
        cache = new HashMap<>();
    }

    public void put(K key, V value, long expirationTimeMillis) {
        long expirationTime = System.currentTimeMillis() + expirationTimeMillis;
        cache.put(key, new CacheEntry<>(value, expirationTime));
    }

    public V get(K key) {
        CacheEntry<V> entry = cache.get(key);
        if (entry != null && entry.isValid()) {
            return entry.getValue();
        }
        return null;
    }

    public void removeExpiredEntries() {
        cache.entrySet().removeIf(entry -> !entry.getValue().isValid());
    }

    private static class CacheEntry<V> {
        private final V value;
        private final long expirationTime;

        public CacheEntry(V value, long expirationTime) {
            this.value = value;
            this.expirationTime = expirationTime;
        }

        public V getValue() {
            return value;
        }

        public boolean isValid() {
            return expirationTime > System.currentTimeMillis();
        }
    }
}
```

The `put()` method adds a new entry to the cache with a given expiration time. The `get()` method retrieves the value corresponding to a key only if the entry is still valid. The `removeExpiredEntries()` method removes all expired entries from the cache.

## Using a custom scheduler

To automatically remove expired entries from the cache, we can use a custom scheduler that periodically calls the `removeExpiredEntries()` method. We can leverage the `ScheduledExecutorService` interface in Java's `java.util.concurrent` package to achieve this.

```java
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class CacheManager<K, V> {
    private Cache<K, V> cache;
    private ScheduledExecutorService scheduler;

    public CacheManager() {
        cache = new Cache<>();
        scheduler = Executors.newScheduledThreadPool(1);
    }

    public void startCacheCleanup(long cleanupIntervalMillis) {
        scheduler.scheduleAtFixedRate(this::cleanupCache, 0, cleanupIntervalMillis, TimeUnit.MILLISECONDS);
    }

    public void stopCacheCleanup() {
        scheduler.shutdown();
    }

    private void cleanupCache() {
        cache.removeExpiredEntries();
    }

    public void put(K key, V value, long expirationTimeMillis) {
        cache.put(key, value, expirationTimeMillis);
    }

    public V get(K key) {
        return cache.get(key);
    }
}
```

The `CacheManager` class encapsulates the cache and scheduler functionality. The `startCacheCleanup()` method starts the cache cleanup task at the specified interval, and the `stopCacheCleanup()` method stops the cleanup task. The `put()` and `get()` methods delegate the corresponding cache operations to the underlying cache object.

## Conclusion

Implementing a cache with time-based expiration using a custom scheduler and HashMap in Java can significantly improve the performance of your applications by reducing data retrieval time. By periodically removing expired entries, you ensure that your cached data remains accurate and up-to-date.

Remember to adjust the expiration time according to the nature and update frequency of your cached data to strike the right balance between performance and freshness.

Happy caching!

**References:**
- [Oracle Java Documentation](https://docs.oracle.com/javase/8/docs/api/index.html)
- [ScheduledExecutorService - Java Documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/concurrent/ScheduledExecutorService.html)

[#java #caching]