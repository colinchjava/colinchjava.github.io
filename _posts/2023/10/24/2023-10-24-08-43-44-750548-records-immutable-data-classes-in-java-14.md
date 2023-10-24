---
layout: post
title: "Records (immutable data classes) in Java 14"
description: " "
date: 2023-10-24
tags: [records]
comments: true
share: true
---

In the world of object-oriented programming, the concept of immutability has gained significant importance. Immutable objects have several benefits, including improved thread safety and simplified code. With the release of Java 14, a new feature called **Records** has been introduced, which simplifies the creation of immutable data classes.

## What are Records?

Records are a new type of class introduced in Java 14 that automatically generate a bunch of useful methods, making it effortless to create immutable data classes. These classes are compact, straightforward, and designed specifically for holding data, rather than behavior.

## Creating a Record

To create a record, you simply need to use the `record` keyword followed by the class name and the list of fields within parentheses. Each field represents a piece of data that the record holds.

Here's an example of a record representing a student:

```java
record Student(String name, int age, String major) { }
```

In the example above, we define a record called `Student` with three fields: `name`, `age`, and `major`. Note that we don't need to manually declare the fields or provide any getter or setter methods. Records automatically generate these methods for us.

## Generated Methods

Records automatically generate several methods, including the `equals()`, `hashCode()`, and `toString()` methods. These generated methods are based on the fields declared in the record.

For example, the `equals()` method checks if all the fields in two record instances are equal. The `hashCode()` method calculates a hash code based on the fields, and the `toString()` method provides a human-readable representation of the record.

## Usage of Records

Records can be used in many scenarios where immutable data classes are required. They are particularly useful when dealing with data transfer objects (DTOs), database entities, configuration settings, and more.

Let's see an example where we use the `Student` record:

```java
Student student = new Student("John Doe", 20, "Computer Science");
System.out.println(student); // Output: Student[name=John Doe, age=20, major=Computer Science]
```

In the code above, we create a new `Student` record instance and print it using the `toString()` method. The output represents the record's fields and values.

## Conclusion

Records are a fantastic addition to Java 14, making it easier to create immutable data classes. They simplify the process of defining and working with data-centric classes. With their automatic generation of useful methods, such as `equals()`, `hashCode()`, and `toString()`, records help reduce the boilerplate code often associated with immutable classes.

By embracing records, developers can write cleaner and more concise code, improving readability and maintainability. They are a tool that can enhance the overall design and architecture of Java applications.

[#java] [#records]