---
layout: post
title: "Abstract methods in anonymous inner classes in Java"
description: " "
date: 2023-09-26
tags: [InnerClasses]
comments: true
share: true
---

In Java, an anonymous inner class is a class without a name that is declared and instantiated at the same time. These classes are typically used when we need to implement a class or interface for a one-time use. 

One common use case for anonymous inner classes is to define and implement abstract methods. Abstract methods are defined in abstract classes or interfaces and do not have an implementation. Instead, the implementation is provided by concrete classes that extend the abstract class or implement the interface.

To define an anonymous inner class that implements an abstract method, you can use the following syntax:

```java
abstract class MyAbstractClass {
    abstract void myMethod();
}

public class Main {
    public static void main(String[] args) {
        MyAbstractClass obj = new MyAbstractClass() {
            @Override
            void myMethod() {
                // implementation of the abstract method
            }
        };

        obj.myMethod(); // calling the implemented method
    }
}
```

In the example above, we have an abstract class `MyAbstractClass` with an abstract method `myMethod()`. Inside the `main()` method, we define an anonymous inner class that extends `MyAbstractClass` and provides an implementation for `myMethod()`.

The syntax for creating an anonymous inner class is similar to creating a regular class instance, except that we provide the implementation of the abstract method(s) directly inside the class declaration.

Once the anonymous inner class is defined, we can create an instance of it and call the implemented method. In this case, we create an object `obj` of `MyAbstractClass` and call `myMethod()` on it.

Anonymous inner classes are convenient when we need to provide a one-time implementation for an abstract method. They are often used in event handling, where we need to define a callback or listener for a specific event.

By using anonymous inner classes, we can avoid the need to create a separate class file for a single implementation, making our code more concise and readable.

#### #Java #InnerClasses