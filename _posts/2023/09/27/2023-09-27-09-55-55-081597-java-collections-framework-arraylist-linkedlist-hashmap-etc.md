---
layout: post
title: "Java collections framework (ArrayList, LinkedList, HashMap, etc.)"
description: " "
date: 2023-09-27
tags: [JavaCollectionsFramework, ArrayList]
comments: true
share: true
---

Java Collections Framework is a powerful set of classes and interfaces provided by Java to easily manage and manipulate collections of objects. It offers a wide range of data structures such as ArrayList, LinkedList, HashSet, HashMap, and many more, making it easier for developers to handle and organize data efficiently.

## ArrayList

ArrayList is a dynamic array implementation in Java. It provides a resizable-array implementation of the List interface. ArrayLists can grow or shrink dynamically as elements are added or removed. This makes it suitable for scenarios where we need to frequently modify the size of the collection.

```java
// Example usage of ArrayList
import java.util.ArrayList;

public class ArrayListExample {
    public static void main(String[] args) {
        ArrayList<String> fruits = new ArrayList<>();

        // Adding elements to the ArrayList
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Orange");

        // Accessing elements from the ArrayList
        System.out.println(fruits.get(0)); // Output: Apple

        // Modifying elements in the ArrayList
        fruits.set(1, "Grapes");
        
        // Removing elements from the ArrayList
        fruits.remove(0);

        // Iterating over the ArrayList
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
    }
}
```

## LinkedList

LinkedList is a doubly-linked list implementation in Java. Unlike ArrayList, it provides efficient insertion and deletion operations due to its underlying data structure. However, accessing elements by index is slower compared to ArrayList.

```java
// Example usage of LinkedList
import java.util.LinkedList;

public class LinkedListExample {
    public static void main(String[] args) {
        LinkedList<String> countries = new LinkedList<>();

        // Adding elements to the LinkedList
        countries.add("India");
        countries.add("USA");
        countries.add("UK");
        
        // Accessing elements from the LinkedList
        System.out.println(countries.get(0)); // Output: India
        
        // Modifying elements in the LinkedList
        countries.set(1, "Canada");
        
        // Removing elements from the LinkedList
        countries.remove(0);

        // Iterating over the LinkedList
        for (String country : countries) {
            System.out.println(country);
        }
    }
}
```

## HashMap

HashMap is an implementation of the Map interface in Java. It stores key-value pairs and allows efficient retrieval of values based on the key. HashMap provides constant-time performance for basic operations like putting and getting elements.

```java
// Example usage of HashMap
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        HashMap<Integer, String> students = new HashMap<>();
        
        // Adding elements to the HashMap
        students.put(1, "John");
        students.put(2, "Emma");
        students.put(3, "Michael");
        
        // Accessing elements from the HashMap
        System.out.println(students.get(2)); // Output: Emma
        
        // Modifying elements in the HashMap
        students.put(1, "Alice");
        
        // Removing elements from the HashMap
        students.remove(3);
        
        // Iterating over the HashMap
        for (int id : students.keySet()) {
            String name = students.get(id);
            System.out.println("ID: " + id + ", Name: " + name);
        }
    }
}
```

The Java Collections Framework provides a wide variety of data structures that cater to different use cases. Understanding these data structures and their characteristics can greatly enhance your ability to write efficient and scalable code.

#JavaCollectionsFramework #ArrayList #LinkedList #HashMap