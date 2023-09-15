---
layout: post
title: "Exploring the concept of functional programming with Java objects"
description: " "
date: 2023-09-15
tags: [functionalprogramming, java]
comments: true
share: true
---

Functional programming is a programming paradigm that focuses on the evaluation of functions rather than changing state or mutating data. While languages like Haskell and Lisp are commonly associated with functional programming, you can also leverage functional programming concepts in traditional object-oriented languages like Java.

In this blog post, we will explore how to apply functional programming principles with Java objects, showcasing some of the features and techniques that Java provides.

## Immutable Objects
One of the important concepts in functional programming is immutability, where objects cannot be changed once they are created. In Java, we can create immutable objects by following a few guidelines:

1. **Declare class attributes as final**: By marking the attributes of a class as final, you ensure that their values cannot be modified once they are set during object creation.
   
2. **Create getter methods without corresponding setter methods**: By omitting the setter methods, you prevent any external modifications to the object's state.

For example, let's create an immutable `Person` class in Java:

```java
public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

## Lambda Expressions
Another powerful feature introduced in Java 8 is the lambda expressions. Lambda expressions allow us to write inline functions, making it easier to implement functional programming concepts.

Let's take a look at an example where we use a lambda expression to sort a list of persons by age:

```java
List<Person> persons = new ArrayList<>();
// Add persons to the list...

persons.sort((p1, p2) -> p1.getAge() - p2.getAge());
```

In the above code snippet, we use the `sort` method from the `List` interface and pass a lambda expression as the comparison function.

## Functional Interfaces
Java provides a set of functional interfaces that enable functional programming constructs. One such interface is the `Predicate` interface, which represents a condition that can be checked against an object.

Let's illustrate this with an example where we filter a list of persons based on their age using a `Predicate`:
   
```java
List<Person> adults = filter(persons, person -> person.getAge() >= 18);

public static List<Person> filter(List<Person> persons, Predicate<Person> predicate) {
    List<Person> filteredPersons = new ArrayList<>();
    for (Person person : persons) {
        if (predicate.test(person)) {
            filteredPersons.add(person);
        }
    }
    return filteredPersons;
}
```

In the above code, we define a `filter` function that takes a list of persons and a `Predicate` as parameters. We iterate over the list and apply the predicate to each person, only including those that satisfy the condition in the resulting filtered list.

## Conclusion
Although Java is primarily an object-oriented language, it provides features and constructs that allow you to embrace functional programming concepts. By leveraging immutability, lambda expressions, and functional interfaces, you can write more concise and expressive code that follows the principles of functional programming.

#functionalprogramming #java