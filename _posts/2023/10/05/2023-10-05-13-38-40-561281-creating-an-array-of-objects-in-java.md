---
layout: post
title: "Creating an array of objects in Java"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

In Java, arrays are used to store multiple values of the same data type. While it is common to create arrays of primitive data types like integers or strings, you can also create arrays of objects. This allows you to store instances of a class in an array.

To create an array of objects in Java, follow these steps:

## 1. Declare the Array Variable

Declare a variable to hold the array. The variable type should be the class name of the objects you want to store in the array, followed by square brackets `[]`. For example, if you want to create an array of `Person` objects, you would declare the array variable as follows:

```java
Person[] peopleArray;
```

## 2. Initialize the Array

Next, initialize the array by creating a new instance of the array and specifying the number of elements it should be able to hold. Use the `new` keyword followed by the class name and the desired array size enclosed in square brackets `[]`. For example, if you want to create an array that can hold ten `Person` objects, you would initialize the array as follows:

```java
peopleArray = new Person[10];
```

## 3. Create Objects

After initializing the array, you can create individual objects of the class and store them in the array. To do this, use the array variable followed by the index position enclosed in square brackets `[]`, and assign the new object to that index. For example, to create a new `Person` object and store it in the first position of the array, you would write:

```java
peopleArray[0] = new Person("John", 25);
```

You can repeat this step to create and store more objects in the array at different index positions.

## Complete Example

Here's a complete example that demonstrates how to create an array of `Person` objects:

```java
public class Main {
    public static void main(String[] args) {
        Person[] peopleArray = new Person[3];

        peopleArray[0] = new Person("John", 25);
        peopleArray[1] = new Person("Jane", 30);
        peopleArray[2] = new Person("Alice", 20);

        for (Person person : peopleArray) {
            System.out.println(person.getName() + " - " + person.getAge());
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

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

In this example, an array of `Person` objects is created with a size of 3. Three `Person` objects are then created and stored at different index positions in the array. Finally, the objects in the array are printed to the console.

## Conclusion

By following the steps outlined above, you can create an array of objects in Java. This allows you to store multiple instances of a class in a single data structure, opening up various possibilities for organizing and manipulating your data. Happy coding!

#java #programming