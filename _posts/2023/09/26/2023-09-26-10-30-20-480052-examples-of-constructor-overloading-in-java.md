---
layout: post
title: "Examples of constructor overloading in Java"
description: " "
date: 2023-09-26
tags: [Constructors]
comments: true
share: true
---

In Java, constructor overloading allows a class to have multiple constructors with different parameters. This enables us to create objects of the same class using different sets of input values. When a constructor is overloaded, each constructor can perform different initialization tasks depending on the arguments passed.

## Syntax

```java
public class ClassName {
    
    // Constructors
    
    public ClassName() {
        // Default constructor code
    }
    
    public ClassName(type1 param1) {
        // Constructor code
    }
    
    public ClassName(type2 param2) {
        // Constructor code
    }
    
    // Additional constructors
    
    // ...
}
```

## Example

Let's consider the example of a `Person` class that represents a person's information, such as their name and age. We can define different constructors to initialize the object based on different input parameters.

```java
public class Person {
    
    private String name;
    private int age;
    
    public Person() {
        name = "Unknown";
        age = 0;
    }
    
    public Person(String personName) {
        name = personName;
        age = 0;
    }
    
    public Person(String personName, int personAge) {
        name = personName;
        age = personAge;
    }
    
    // Other methods
    
    //...
}
```

In the example above, the `Person` class has three constructors:

1. The default constructor sets `name` to "Unknown" and `age` to 0.
2. The constructor with a single parameter `personName` sets `name` to the specified value and `age` to 0.
3. The constructor with two parameters `personName` and `personAge` sets both `name` and `age` to the specified values.

We can now create `Person` objects based on the required parameters:

```java
Person person1 = new Person(); // Using the default constructor
Person person2 = new Person("John"); // Using the constructor with a single parameter
Person person3 = new Person("Alice", 25); // Using the constructor with two parameters
```

By overloading the constructors, we provide flexibility to create objects with varying initializations depending on the requirements.

#Java #Constructors