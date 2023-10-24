---
layout: post
title: "Enhanced records (immutable data classes) in Java 18"
description: " "
date: 2023-10-24
tags: [EnhancedRecords]
comments: true
share: true
---

Java 18 introduces a new feature called **enhanced records** that allows you to define immutable data classes more concisely. The new syntax simplifies the creation of simple data classes by eliminating boilerplate code for getters, setters, and equals/hashCode methods. In this blog post, we will explore how enhanced records work and how they can benefit your Java code.

## What are Enhanced Records?

Enhanced records in Java provide a concise way to define classes that are primarily used for storing data. They are designed to be immutable, meaning that once created, their state cannot be modified. The immutability of records ensures better code stability, thread safety, and simpler debugging.

## Creating an Enhanced Record

To define an enhanced record, you simply use the `record` keyword followed by the class name and a list of record components (fields). Each component is defined using the `type name` syntax.

```java
public record Person(String name, int age) {}
```

In the example above, we define a `Person` record with two components: `name` of type `String` and `age` of type `int`. By default, records automatically generate:

- Constructors that accept values for each record component
- Getter methods for each record component
- `equals()`, `hashCode()`, and `toString()` methods based on the record components

## Immutable by Default

Records are implicitly `final` and the record components are implicitly `final`. This ensures that the state of a record instance cannot be modified once it is created. If you try to modify a record's field, it will result in a compilation error.

```java
Person person = new Person("John", 25);
person.name = "Jane"; // Compilation error: cannot assign a value to final variable 'name'
```

## Simplified Record Syntax

Enhanced records in Java 18 also introduce a simplified record syntax, allowing you to define records in a more compact form. 

```java
public record Person(String name, int age) {}
```

The simplified syntax omits the constructor, getter, and equals/hashCode methods altogether. However, be aware that using the simplified syntax limits you from adding custom logic to these methods. If you need custom behavior, you can still use the full syntax for defining records.

## Benefits of Enhanced Records

Enhanced records bring several benefits to Java developers:

1. **Conciseness**: The new syntax eliminates boilerplate code, making your data classes more readable and maintaining a smaller codebase.
2. **Immutable by Default**: Records enforce immutability, ensuring safer code with fewer bugs related to mutable state.
3. **Automatic Generation**: Records automatically generate constructors, getters, setters, `equals()`, `hashCode()`, and `toString()` methods, reducing manual effort and reducing the risk of errors.

## Conclusion

Enhanced records in Java 18 provide an elegant and concise way to define immutable data classes. They simplify the creation of simple data structures, eliminate boilerplate code, and enforce immutability. With their automatic generation of commonly used methods, they improve code readability and reduce the risk of errors. Take advantage of this new feature in Java 18 to write cleaner and more robust code.

For more information, you can refer to the [Java 18 JEP-395](https://openjdk.java.net/jeps/395) documentation.

\#Java #EnhancedRecords