---
layout: post
title: "Understanding the usage of wrapper classes in Java generics"
description: " "
date: 2023-09-14
tags: [Generics]
comments: true
share: true
---

Generics in Java provide a way to create reusable code by **defining classes, interfaces, and methods** that can work with different types of data. One of the key features of generics is the ability to use **wrapper classes** to work with primitive types.

Java provides **primitive data types** like `int`, `float`, `char`, etc., which are not compatible with generics. To overcome this limitation, **wrapper classes** such as `Integer`, `Float`, `Character` are used. These wrapper classes encapsulate the primitive types and provide methods and functionality to work with them.

Let's take an example of a simple generic class `Box`:

```java
public class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }
}
```
In the above code, the `Box` class is a generic class that can hold any type of object. But what if we want to use it to store an `int`? Here is where the wrapper class `Integer` comes into play.

Using wrapper classes, we can modify the `Box` class to store and retrieve the `int` type:

```java
public class Box<T> {
    private T value;

    public Box(T value) {
        this.value = value;
    }

    public T getValue() {
        return value;
    }

    public void setValue(T value) {
        this.value = value;
    }
}

public class Main {
    public static void main(String[] args) {
        Box<Integer> box = new Box<>(42); // Creating a Box with Integer wrapper class
        int value = box.getValue(); // Retrieving the stored int value
        System.out.println(value); // Output: 42
    }
}
```
In this example, we create an instance of the `Box` class using the `Integer` wrapper class. We can then retrieve the stored value as an `int` using the `getValue` method. 

Wrapper classes provide a convenient way to work with primitive types in a generic context. They allow us to use generics effectively, even with non-object types.

By using wrapper classes, we can handle any type of data within the framework of Java generics, making our code more flexible and reusable.

#Java #Generics