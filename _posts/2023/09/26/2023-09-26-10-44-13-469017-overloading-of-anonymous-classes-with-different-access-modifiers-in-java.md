---
layout: post
title: "Overloading of anonymous classes with different access modifiers in Java"
description: " "
date: 2023-09-26
tags: [Java, AnonymousClasses]
comments: true
share: true
---

In Java, anonymous classes provide a way to create a single-use class without explicitly naming it. They are often used in situations where a class is needed to implement an interface or extend a class, but no need exists to define it separately.

One interesting feature of anonymous classes is that we can overload their constructors by providing different numbers or types of parameters. In addition to this, we can also specify different access modifiers for these overloaded constructors.

Let's take a look at an example to understand how overloading of anonymous classes with different access modifiers works:

```java
public class Main {
    public static void main(String[] args) {
        // Overloaded anonymous class with public constructor
        MyClass publicInstance = new MyClass() {
            public void display() {
                System.out.println("Public Instance");
            }
        };
        publicInstance.display();

        // Overloaded anonymous class with private constructor
        MyClass privateInstance = new MyClass() {
            private void display() {
                System.out.println("Private Instance");
            }
        };
        privateInstance.display(); // Error: display() has private access in MyClass
    }

    static class MyClass {
        public void display() {
            System.out.println("Default Instance");
        }
    }
}
```

In the above code, we defined an anonymous class `MyClass` inside the `Main` class. We then created two instances of this anonymous class, `publicInstance` and `privateInstance`, by overloading the constructors.

The `publicInstance` instance was created with a public constructor, and its `display()` method was overridden to print "Public Instance". When calling the `display()` method on `publicInstance`, it successfully prints the desired output.

On the other hand, the `privateInstance` instance was created with a private constructor, and its `display()` method was also overridden to print "Private Instance". However, when attempting to call the `display()` method on `privateInstance`, a compile-time error occurs because the method has private access in `MyClass`.

In conclusion, we can overload the constructors of anonymous classes with different access modifiers in Java. However, we must ensure that the overridden methods in these anonymous classes have the same or less restrictive access modifiers as the original methods in the base class.

#Java #AnonymousClasses #AccessModifiers