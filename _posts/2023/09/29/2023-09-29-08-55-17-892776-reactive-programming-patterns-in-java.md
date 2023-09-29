---
layout: post
title: "Reactive programming patterns in Java"
description: " "
date: 2023-09-29
tags: [reactiveprogramming, javadevelopment]
comments: true
share: true
---

Reactive programming is an approach to writing software that allows for the handling of asynchronous and event-driven scenarios. It focuses on creating systems that are highly responsive, resilient, and scalable by using **reactive programming patterns**.

In Java, there are several libraries and frameworks that enable developers to implement reactive programming patterns. These patterns help in handling data streams, event-driven scenarios, and managing asynchronous tasks efficiently. In this blog post, we will explore some of the most commonly used reactive programming patterns in Java.

## 1. Observer Pattern

The **Observer pattern** is a widely used reactive pattern that provides a one-to-many relationship between an Observable (subject) and its Observers. In this pattern, the Observers subscribe to changes in the Observable, and are notified whenever the Observable's state changes.

### Code Example:

```java
import java.util.Observable;
import java.util.Observer;

public class Subject extends Observable {
    private int state; // Observable state

    public void setState(int state) {
        this.state = state;
        setChanged(); // Notify Observers of state change
        notifyObservers(state);
    }
}

public class ObserverDemo {
    public static void main(String[] args) {
        Subject subject = new Subject();

        // Create Observers
        Observer observer1 = (o, arg) -> System.out.println("Observer 1: " + arg);
        Observer observer2 = (o, arg) -> System.out.println("Observer 2: " + arg);

        // Subscribe Observers to Subject
        subject.addObserver(observer1);
        subject.addObserver(observer2);

        // Update Subject state
        subject.setState(10);
    }
}
```

## 2. Flux and Mono

**Flux** and **Mono** are fundamental classes in **Project Reactor** library, which is an implementation of the **Reactive Streams specification**. These classes provide the building blocks for reactive programming in Java.

- **Flux** represents a stream of 0 to N items and emits them asynchronously.
- **Mono** represents a stream with at most one item and emits it asynchronously.

### Code Example:

```java
import reactor.core.publisher.Flux;
import reactor.core.publisher.Mono;

public class ReactiveStreamsDemo {
    public static void main(String[] args) {
        Flux<String> fluxStream = Flux.just("Hello", "World", "!");

        fluxStream
            .map(String::toUpperCase) // Transform stream elements
            .doOnNext(System.out::println) // Print each element
            .subscribe();
        
        Mono<String> monoStream = Mono.just("Hello Reactive World!");

        monoStream
            .map(String::toLowerCase) // Transform stream element
            .doOnSuccess(System.out::println) // Print the element on successful completion
            .subscribe();
    }
}
```

These are just a couple of reactive programming patterns that can be implemented in Java. By leveraging reactive programming patterns and libraries, developers can build more efficient and scalable systems that are better equipped to handle asynchronous and event-driven scenarios.

#reactiveprogramming #javadevelopment