---
layout: post
title: "Using custom objects as values in a HashMap in Java"
description: " "
date: 2023-10-23
tags: [hashmap]
comments: true
share: true
---

In Java, the `HashMap` class allows you to store key-value pairs where each key is unique. By default, `HashMap` allows storing any type of object as a value, including custom objects. This allows you to create a collection of custom objects and easily retrieve them using a specific key.

To use custom objects as values in a `HashMap`, you need to follow these steps:

### Step 1: Create a Custom Object class

First, create a custom class that represents the object you want to store in the `HashMap`. Here is an example of a `Person` class with properties for `name` and `age`:

```java
public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Getters and setters

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```

### Step 2: Create and Populate the HashMap

Next, create an instance of the `HashMap` class and populate it with custom objects. Here's an example that creates a `HashMap` with `String` keys and `Person` objects as values:

```java
import java.util.HashMap;

public class Main {
    public static void main(String[] args) {
        HashMap<String, Person> personMap = new HashMap<>();

        Person john = new Person("John Doe", 30);
        Person jane = new Person("Jane Smith", 25);

        personMap.put("John", john);
        personMap.put("Jane", jane);
    }
}
```

### Step 3: Retrieve Objects from the HashMap

You can retrieve custom objects from the `HashMap` using the specified keys. Here's an example that retrieves the `Person` object using the key `"John"`:

```java
Person retrievedPerson = personMap.get("John");
System.out.println(retrievedPerson.getName()); // Output: John Doe
System.out.println(retrievedPerson.getAge()); // Output: 30
```

### Conclusion

Using custom objects as values in a `HashMap` allows you to organize and retrieve data effectively. By providing unique keys, you can easily access the objects stored in the `HashMap`. This feature enhances the flexibility and functionality of the `HashMap` class in Java.

For more details, refer to the official Java documentation on [HashMap](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html).

#java #hashmap