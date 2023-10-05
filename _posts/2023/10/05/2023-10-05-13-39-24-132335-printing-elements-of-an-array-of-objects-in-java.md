---
layout: post
title: "Printing elements of an array of objects in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

When working with arrays of objects in Java, it is common to want to print the elements of the array for debugging or informational purposes. This can be achieved by iterating over the array and printing each element.

Here's an example of how to print the elements of an array of objects in Java:

```java
public class Main {
    public static void main(String[] args) {
        // Create an array of objects
        Person[] people = new Person[3];
        people[0] = new Person("John", 25);
        people[1] = new Person("Jane", 30);
        people[2] = new Person("Michael", 35);

        // Iterate over the array and print each element
        for (Person person : people) {
            System.out.println(person);
        }
    }
}

class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
}
```

In the above example, we have an array of `Person` objects. We initialize the array with three `Person` objects and then use a `for-each` loop to iterate over the array. Within the loop, we call the `toString()` method on each `Person` object and print it using the `System.out.println()` statement.

The `Person` class overrides the `toString()` method to provide a customized string representation of the object. This is done by concatenating the `name` and `age` fields in the `toString()` method.

When you run the program, it will output the following:

```
Person{name='John', age=25}
Person{name='Jane', age=30}
Person{name='Michael', age=35}
```

By following this approach, you can easily print the elements of an array of objects in Java. It is a useful technique for debugging and understanding the contents of your arrays.