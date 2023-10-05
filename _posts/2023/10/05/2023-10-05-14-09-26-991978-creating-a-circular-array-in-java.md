---
layout: post
title: "Creating a circular array in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with arrays in Java, it can be useful to have a circular array that allows you to efficiently cycle through elements without needing to resize or shift elements. In this blog post, we will explore how to create a circular array in Java.

## What is a Circular Array?

A circular array is an array where the last element is connected to the first element, creating a circular structure. This means that when you reach the end of the array, the next element is the first element, and when you reach the beginning of the array, the previous element is the last element.

## Implementation of a Circular Array

To create a circular array in Java, we can use a combination of an array and a modulus operator (%). The modulus operator allows us to wrap around the array indices, effectively creating a circular structure.

Here's an example implementation of a circular array class in Java:

```java
public class CircularArray<T> {
    private T[] array;
    private int size;
    private int head;

    public CircularArray(int size) {
        this.array = (T[]) new Object[size];
        this.size = size;
        this.head = 0;
    }

    public T get(int index) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException();
        }
        return array[(head + index) % size];
    }

    public void set(int index, T element) {
        if (index < 0 || index >= size) {
            throw new IndexOutOfBoundsException();
        }
        array[(head + index) % size] = element;
    }

    public void rotateRight() {
        head = (head + 1) % size;
    }

    public void rotateLeft() {
        head = (head - 1 + size) % size;
    }
}
```

## Usage Example

Let's see how we can use the `CircularArray` class we implemented:

```java
public class Main {
    public static void main(String[] args) {
        CircularArray<String> circularArray = new CircularArray<>(5);

        circularArray.set(0, "A");
        circularArray.set(1, "B");
        circularArray.set(2, "C");
        circularArray.set(3, "D");
        circularArray.set(4, "E");

        // Print elements in order
        for (int i = 0; i < 5; i++) {
            System.out.println(circularArray.get(i));
        }

        // Rotate to the right
        circularArray.rotateRight();

        // Print elements after rotation
        for (int i = 0; i < 5; i++) {
            System.out.println(circularArray.get(i));
        }
    }
}
```

Output:
```
A
B
C
D
E
B
C
D
E
A
```

As you can see from the output, the circular array allows us to cycle through elements seamlessly, even after rotating.

## Conclusion

In this blog post, we learned how to create a circular array in Java using an array and the modulus operator. A circular array can be a useful data structure in certain scenarios, allowing efficient cycling through elements without the need for resizing or shifting.

Using the `CircularArray` class we implemented, you can easily create your own circular arrays in Java and take advantage of the circular structure they provide.

#programming #java