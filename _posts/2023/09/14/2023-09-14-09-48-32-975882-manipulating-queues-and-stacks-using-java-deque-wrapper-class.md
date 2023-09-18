---
layout: post
title: "Manipulating queues and stacks using Java Deque wrapper class"
description: " "
date: 2023-09-14
tags: [queues, stacks]
comments: true
share: true
---

In Java, the `Deque` interface is a double-ended queue that provides functionality for manipulating both queues and stacks. It supports adding, removing, and inspecting elements from both ends of the queue, allowing us to implement various queue and stack data structures.

Here, we'll explore how to use the `Deque` interface to implement queues and stacks in Java.

## Queue Implementation

To implement a queue using the `Deque` interface, we can utilize the `add()` method to add elements at the end of the queue, and the `remove()` method to remove elements from the front of the queue.

```java
import java.util.Deque;
import java.util.LinkedList;

public class QueueExample {
    public static void main(String[] args) {
        Deque<String> queue = new LinkedList<>();

        // Adding elements to the queue
        queue.add("Apple");
        queue.add("Banana");
        queue.add("Cherry");

        // Removing elements from the queue
        String firstElement = queue.remove();
        System.out.println("Removed element: " + firstElement);

        // Peek the first element without removing
        String peekElement = queue.peek();
        System.out.println("Peeked element: " + peekElement);
    }
}
```

In the above example, we first import the required classes. Then, we create an instance of the `Deque` interface using the `LinkedList` class, which provides a doubly-linked list implementation of the `Deque` interface.

We add elements to the queue using the `add()` method, and remove elements from the front of the queue using the `remove()` method. The `peek()` method allows us to inspect the first element without removing it.

## Stack Implementation

To implement a stack using the `Deque` interface, we can also use the `add()` method to add elements at the beginning of the stack, and the `remove()` method to remove elements from the beginning of the stack.

```java
import java.util.Deque;
import java.util.LinkedList;

public class StackExample {
    public static void main(String[] args) {
        Deque<String> stack = new LinkedList<>();

        // Pushing elements to the stack
        stack.addFirst("Apple");
        stack.addFirst("Banana");
        stack.addFirst("Cherry");

        // Popping elements from the stack
        String firstElement = stack.removeFirst();
        System.out.println("Popped element: " + firstElement);

        // Peek the top element without popping
        String peekElement = stack.peekFirst();
        System.out.println("Peeked element: " + peekElement);
    }
}
```

Similar to the queue implementation, we create an instance of the `Deque` interface using the `LinkedList` class. Instead of adding elements using the `add()` method, we use `addFirst()` to add elements at the beginning of the stack. The `removeFirst()` method is used to remove elements from the top of the stack, and `peekFirst()` allows us to peek at the top element without removing it.

By utilizing the `Deque` interface, we can implement both queues and stacks in Java. Whether you need a data structure that follows the FIFO (First-In, First-Out) principle like queues or follows the LIFO (Last-In, First-Out) principle like stacks, the `Deque` interface provides the necessary operations to manipulate the data efficiently.

#java #queues #stacks