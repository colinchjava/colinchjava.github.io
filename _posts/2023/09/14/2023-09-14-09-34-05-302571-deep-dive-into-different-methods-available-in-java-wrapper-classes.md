---
layout: post
title: "Deep dive into different methods available in Java wrapper classes"
description: " "
date: 2023-09-14
tags: [programming]
comments: true
share: true
---

Java provides a set of wrapper classes that wrap the primitive data types and provide additional functionality. These wrapper classes, such as `Integer`, `Double`, `Character`, etc., are quite useful when working with objects or when we need to perform operations on primitive data types.

In this article, we will take a deep dive into some of the commonly used methods available in Java wrapper classes.

## Common Methods in Java Wrapper Classes

### Converting Wrappers to Primitive Data Types

One of the most common operations is converting wrapper objects to their corresponding primitive data types. Java provides several methods to perform these conversions:

```java
Integer intValue = new Integer(10);
int primitiveValue = intValue.intValue();
System.out.println("Primitive Value: " + primitiveValue);
```

The `intValue()` method returns the wrapped value as an `int`.

### Converting Wrappers to String

Java wrapper classes also provide methods to convert the wrapped value to a string representation:

```java
Integer intValue = new Integer(10);
String stringValue = intValue.toString();
System.out.println("String Value: " + stringValue);
```

The `toString()` method returns the string representation of the wrapped value.

### Converting String to Wrappers

Java wrapper classes also allow converting string values to wrapper objects:

```java
String stringValue = "15";
Integer intValue = Integer.valueOf(stringValue);
System.out.println("Integer Value: " + intValue);
```

The `valueOf()` method returns the wrapper object corresponding to the given string representation.

### Performing Arithmetic Operations

Wrapper classes in Java also provide methods to perform arithmetic operations:

```java
Integer intValue1 = new Integer(5);
Integer intValue2 = new Integer(10);

// Addition
Integer sum = intValue1 + intValue2;
System.out.println("Sum: " + sum);

// Subtraction
Integer difference = intValue2 - intValue1;
System.out.println("Difference: " + difference);

// Multiplication
Integer product = intValue1 * intValue2;
System.out.println("Product: " + product);
```

In the above example, we perform addition, subtraction, and multiplication operations using the `+`, `-`, and `*` operators respectively.

### Comparing Wrapper Values

Wrapper classes also support comparison operations through methods like `equals()`, `compareTo()`, and `compareToIgnoreCase()`. Here's an example:

```java
Integer intValue1 = new Integer(5);
Integer intValue2 = new Integer(10);

// Using equals()
if (intValue1.equals(intValue2)) {
    System.out.println("Values are equal");
} else {
    System.out.println("Values are not equal");
}

// Using compareTo()
int comparison = intValue1.compareTo(intValue2);
if (comparison == 0) {
    System.out.println("Values are equal");
} else if (comparison < 0) {
    System.out.println("Value 1 is less than Value 2");
} else {
    System.out.println("Value 1 is greater than Value 2");
}
```

The `equals()` method checks if two wrapper objects are equal, while `compareTo()` compares two wrapper objects based on their values.

## Conclusion

In this article, we explored some of the common methods available in Java wrapper classes. These methods allow us to convert wrappers to primitive data types, perform arithmetic operations, compare values, and more. Understanding and utilizing these methods will greatly enhance our ability to work with wrapper classes effectively.

#programming #java