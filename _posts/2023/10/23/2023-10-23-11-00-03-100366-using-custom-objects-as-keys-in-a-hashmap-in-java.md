---
layout: post
title: "Using custom objects as keys in a HashMap in Java"
description: " "
date: 2023-10-23
tags: [References]
comments: true
share: true
---

In Java, the `HashMap` is a popular data structure that allows us to store and retrieve key-value pairs efficiently. By default, the keys used in a `HashMap` are of type `Object`, but it is also possible to use custom objects as keys. This can be useful when we want to store and retrieve values based on certain attributes of an object.

To use custom objects as keys in a `HashMap`, we need to ensure that these objects fulfill the requirements for serving as keys. Here are the steps to follow:

## 1. Implement the `hashCode()` method

The `hashCode()` method is used by the `HashMap` to generate an integer value that represents the object's key. It is important to implement this method correctly to ensure that keys are unique and distributed evenly across the hash table. 

```java
@Override
public int hashCode() {
    // Your implementation here
}
```
Remember to consider all the attributes of your object that define its uniqueness while generating the hash code.

## 2. Implement the `equals()` method

The `equals()` method is used by the `HashMap` to compare keys for equality. This method is critical for correctly retrieving values from the map.

```java
@Override
public boolean equals(Object obj) {
    // Your implementation here
}
```

Make sure to compare all the relevant attributes of your custom object to determine if they are equal.

## 3. Use the custom object as a key in the HashMap

Once you have implemented the `hashCode()` and `equals()` methods, you can use your custom object as a key in the `HashMap`. Here is an example:

```java
Map<MyObject, String> map = new HashMap<>();

MyObject key1 = new MyObject("123");
MyObject key2 = new MyObject("456");

map.put(key1, "Value 1");
map.put(key2, "Value 2");

String value1 = map.get(key1);
String value2 = map.get(key2);
```

Remember to ensure that the custom object remains immutable after being used as a key in the `HashMap`. Modifying the object might cause inconsistencies in its hash code, resulting in incorrect retrieval of values from the map.

Using custom objects as keys in a `HashMap` allows us to build powerful data structures and access values based on specific attributes of the objects. Remember to implement the `hashCode()` and `equals()` methods correctly to ensure the desired behavior.

#References
- Oracle Java Documentation: [HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)
- Baeldung: [Custom Objects as Keys in a Java HashMap](https://www.baeldung.com/java-hashmap-custom-object-keys)