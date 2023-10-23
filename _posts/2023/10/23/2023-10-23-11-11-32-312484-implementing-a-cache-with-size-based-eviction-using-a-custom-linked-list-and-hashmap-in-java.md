---
layout: post
title: "Implementing a cache with size-based eviction using a custom linked list and HashMap in Java"
description: " "
date: 2023-10-23
tags: [References, Least]
comments: true
share: true
---

Caching is a common technique used in applications to improve performance by storing frequently accessed data in a faster and more accessible location. In this blog post, we will discuss how to implement a cache with size-based eviction using a custom linked list and HashMap in Java.

## Table Of Contents
- [Introduction](#introduction)
- [The Cache Implementation](#the-cache-implementation)
- [Eviction Strategy](#eviction-strategy)
- [Code Example](#code-example)
- [Conclusion](#conclusion)

<a name="introduction"></a>
## Introduction
A cache is an in-memory data structure that stores a subset of data that is typically expensive to retrieve or generate. By keeping frequently accessed data in memory, we can reduce the latency associated with fetching the data from disk or generating it from scratch.

One common challenge with caching is that the memory available for caching is limited. When the cache reaches its maximum size, we need to remove some items to make room for new ones. This is where the eviction strategy comes into play.

<a name="the-cache-implementation"></a>
## The Cache Implementation
To implement a cache with size-based eviction, we can use a combination of a custom linked list and a HashMap.

The custom linked list will help us maintain the order of items in the cache, with the most recently used items at the front and the least recently used items at the end. The HashMap will provide us with fast access to the items in the cache.

The basic operations we need to support in our cache implementation are:
- Get(key): Retrieve the value associated with the given key from the cache.
- Put(key, value): Add or update the value associated with the given key in the cache.
- Evict(): Remove the least recently used item from the cache when it reaches its maximum size.

<a name="eviction-strategy"></a>
## Eviction Strategy
In a size-based eviction strategy, we need to identify the least recently used item in the cache to remove it and make room for new items. To achieve this, we can use a custom linked list.

Whenever a key is accessed or added in the cache, we move the corresponding node to the front of the linked list. This way, the most recently used items are always at the front, and the least recently used items are at the end.

When the cache reaches its maximum size, we can simply remove the node from the end of the linked list, as it represents the least recently used item.

<a name="code-example"></a>
## Code Example
Here's an example implementation of a cache with size-based eviction in Java:

```java
import java.util.HashMap;

public class LRUCache<K, V> {
    private int capacity;
    private HashMap<K, Node<K, V>> cache;
    private Node<K, V> head;
    private Node<K, V> tail;

    public LRUCache(int capacity) {
        this.capacity = capacity;
        this.cache = new HashMap<>();
        head = new Node<>();
        tail = new Node<>();
        head.next = tail;
        tail.prev = head;
    }

    public V get(K key) {
        Node<K, V> node = cache.get(key);
        if (node == null) {
            return null;
        }
        moveNodeToFront(node);
        return node.value;
    }

    public void put(K key, V value) {
        Node<K, V> node = cache.get(key);
        if (node != null) {
            node.value = value;
            moveNodeToFront(node);
        } else {
            if (cache.size() >= capacity) {
                removeTail();
            }
            node = new Node<>(key, value);
            cache.put(key, node);
            addNodeToFront(node);
        }
    }

    private void moveNodeToFront(Node<K, V> node) {
        node.prev.next = node.next;
        node.next.prev = node.prev;
        addNodeToFront(node);
    }

    private void addNodeToFront(Node<K, V> node) {
        node.prev = head;
        node.next = head.next;
        head.next.prev = node;
        head.next = node;
    }

    private void removeTail() {
        Node<K, V> node = tail.prev;
        cache.remove(node.key);
        node.prev.next = tail;
        tail.prev = node.prev;
    }

    private static class Node<K, V> {
        private K key;
        private V value;
        private Node<K, V> prev;
        private Node<K, V> next;

        Node() {
        }

        Node(K key, V value) {
            this.key = key;
            this.value = value;
        }
    }
}
```

In this implementation, we use a generic type `K` for the key and `V` for the value stored in the cache. We maintain a `capacity` variable to keep track of the maximum size of the cache.

The `get` method retrieves the value associated with the specified key from the cache. If the key is found, the corresponding node is moved to the front of the linked list (indicating it's the most recently used item) and the value is returned.

The `put` method adds or updates the value associated with the given key in the cache. If the key already exists, we update its value and move its node to the front. Otherwise, if the cache is full, we remove the least recently used item (represented by the tail node) and add the new item to the front of the linked list.

The `moveNodeToFront`, `addNodeToFront`, and `removeTail` methods are helper methods for manipulating the linked list.

<a name="conclusion"></a>
## Conclusion
By implementing a cache with size-based eviction using a custom linked list and HashMap in Java, we can efficiently store and retrieve frequently accessed data. The eviction strategy based on the least recently used item ensures that the cache does not exceed its size and removes less frequently used items.

This approach can significantly improve the performance of applications that rely on frequently accessed data. Remember to adjust the cache capacity according to the available memory and the nature of the data being cached.

#References
- [Java HashMap Documentation](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html)
- [Linked List Implementation in Java](https://www.geeksforgeeks.org/implementing-a-linked-list-in-java-using-class/)
- [LRU Cache Algorithm](https://en.wikipedia.org/wiki/Cache_replacement_policies#Least_recently_used_(LRU))