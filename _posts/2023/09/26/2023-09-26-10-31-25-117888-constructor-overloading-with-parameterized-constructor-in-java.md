---
layout: post
title: "Constructor overloading with parameterized constructor in Java"
description: " "
date: 2023-09-26
tags: [constructor]
comments: true
share: true
---

Constructors in Java are special methods used for initializing objects of a class. They are called automatically when an object of a class is created. In Java, constructor overloading allows a class to have multiple constructors with different parameters. This allows flexibility in creating objects of the class.

## Why use Constructor Overloading?

Constructor overloading is beneficial when you want to create objects with different initial states or when you want to initialize objects with different sets of values. It eliminates the need for multiple methods to create objects with different initializations.

## Parameterized Constructor

A parameterized constructor is a constructor that takes parameters when creating an object. These parameters can be used to initialize the instance variables of the class. By providing different sets of parameters, you can create objects with different initializations.

Here's an example of a parameterized constructor in Java:

```java
public class Student {
    private String name;
    private int age;
    private String course;

    // Parameterized constructor
    public Student(String name, int age, String course) {
        this.name = name;
        this.age = age;
        this.course = course;
    }

    // Getter methods
    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    public String getCourse() {
        return course;
    }
}
```

In the example above, we have a `Student` class with three instance variables: `name`, `age`, and `course`. The constructor `Student` takes three parameters: `name`, `age`, and `course`. These parameters are used to initialize the respective instance variables of the class.

Using the constructor, we can create objects of the `Student` class with different initializations:

```java
Student student1 = new Student("John Smith", 20, "Computer Science");
Student student2 = new Student("Jane Doe", 22, "Electrical Engineering");
```

In the above example, we create two `Student` objects with different sets of values passed to the constructor. This allows us to initialize the objects with specific values for each instance variable.

## Conclusion

Constructor overloading with parameterized constructors provides flexibility in creating objects with different initializations. It allows you to define multiple constructors with different sets of parameters, providing convenience in object creation.

Using parameterized constructors, you can initialize the instance variables of a class effectively, making your code more efficient and readable.

#java #constructor-overloading