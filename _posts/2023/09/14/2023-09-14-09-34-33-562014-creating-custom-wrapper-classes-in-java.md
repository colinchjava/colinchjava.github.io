---
layout: post
title: "Creating custom wrapper classes in Java"
description: " "
date: 2023-09-14
tags: [WrapperClasses]
comments: true
share: true
---

Java provides a set of predefined wrapper classes for each primitive data type. However, there may be situations where you need to create your own custom wrapper class. In this blog post, we'll explore how to create and use custom wrapper classes in Java.

## What Are Wrapper Classes?

Wrapper classes are used to convert primitive data types into objects. They wrap the primitive value and provide useful methods to manipulate and interact with it. In Java, the wrapper classes for the primitive data types are:

- `Integer` - for `int`
- `Double` - for `double`
- `Boolean` - for `boolean`
- `Character` - for `char`
- `Long` - for `long`
- `Byte` - for `byte`
- `Short` - for `short`
- `Float` - for `float`

## Why Create Custom Wrapper Classes?

While the built-in wrapper classes are sufficient for most scenarios, creating custom wrapper classes can offer additional functionality and customization options. You might want to create a custom wrapper class if you need to add specific methods or behavior to your wrapped data type.

## Creating a Custom Wrapper Class

To create a custom wrapper class, follow these steps:

1. Create a new Java class and define a private instance variable of the primitive data type that you want to wrap. For example, if you want to create a wrapper class for integers, define a private `int` variable.
   
```java
    public class CustomInteger {

        private int value;

        // constructor, methods, and additional functionality
    }
```

2. Implement getter and setter methods for the instance variable. These methods will allow you to get and set the wrapped value.

```java
    public int getValue() {
        return value;
    }

    public void setValue(int value) {
        this.value = value;
    }
```

3. Add any additional methods or functionality that you want to provide with your custom wrapper class. This can include methods for calculations, conversions, or any other operations specific to your use case.

```java
    public int calculateSquare() {
        return value * value;
    }
```

4. Optionally, you can override the `toString()` method to provide a custom string representation of your wrapper class object.

```java
    @Override
    public String toString() {
        return "CustomInteger{" +
                "value=" + value +
                '}';
    }
```

5. Finally, you can use your custom wrapper class in your code by creating objects of your wrapper class and accessing its methods and properties.

```java
    public class Main {
        public static void main(String[] args) {
            CustomInteger customInt = new CustomInteger();
            customInt.setValue(10);
            System.out.println(customInt.getValue()); // Output: 10
            System.out.println(customInt.calculateSquare()); // Output: 100
            System.out.println(customInt.toString()); // Output: CustomInteger{value=10}
        }
    }
```

## Conclusion

Creating custom wrapper classes in Java allows you to add additional functionality and customization options to your wrapped data types. By following the steps outlined in this blog post, you can easily create and use your own custom wrapper classes in your Java projects.

`#Java #WrapperClasses`