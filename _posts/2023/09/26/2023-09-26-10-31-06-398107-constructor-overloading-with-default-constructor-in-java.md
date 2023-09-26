---
layout: post
title: "Constructor overloading with default constructor in Java"
description: " "
date: 2023-09-26
tags: [java, constructoroverloading]
comments: true
share: true
---

Constructor overloading is a feature in Java that allows us to define multiple constructors in a class with different parameters. This enables us to instantiate objects with different sets of initial values depending on our requirements. In addition to this, we can also include a default constructor, which is a constructor with no parameters.

## Default Constructor

A default constructor is automatically provided by the Java compiler if we don't define any constructors explicitly. It takes no arguments and initializes the instance variables to their default values. The default constructor is commonly used to create objects without any initial values.

Here's an example of a default constructor:

```java
class Person {
    private String name;
    private int age;

    // Default Constructor
    public Person() {
        name = "John Doe";
        age = 18;
    }

    public void displayDetails() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Person person = new Person();
        person.displayDetails();
    }
}
```

In the above example, we have a `Person` class with a default constructor. The constructor initializes the `name` to "John Doe" and `age` to 18. 

In the `main` method, we create a `Person` object using the default constructor and call the `displayDetails` method to print the values of the instance variables.

## Overloading Constructors

We can also define multiple constructors in a class with different parameter lists. This allows us to create objects with different initial values depending on which constructor we use. Here's an example:

```java
class Person {
    private String name;
    private int age;

    // Default Constructor
    public Person() {
        name = "John Doe";
        age = 18;
    }

    // Parameterized Constructor
    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public void displayDetails() {
        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
    }
}

public class Main {
    public static void main(String[] args) {
        Person person1 = new Person(); // Using default constructor
        person1.displayDetails();

        Person person2 = new Person("Jane Smith", 25); // Using parameterized constructor
        person2.displayDetails();
    }
}
```

In this example, we have added a parameterized constructor in addition to the default constructor. The parameterized constructor takes `name` and `age` as arguments and initializes the instance variables accordingly.

In the `main` method, we create two `Person` objects - `person1` using the default constructor and `person2` using the parameterized constructor. We then call the `displayDetails` method on both objects to print their details.

## Conclusion

Constructor overloading in Java allows us to create objects with different initial values by defining multiple constructors in a class. This gives us flexibility in instantiating objects based on our requirements. Including a default constructor allows us to create objects without any initial values. By utilizing constructor overloading effectively, we can design more versatile and reusable code. #java #constructoroverloading