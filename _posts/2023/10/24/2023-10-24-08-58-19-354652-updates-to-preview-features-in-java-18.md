---
layout: post
title: "Updates to preview features in Java 18"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

Java 18, the upcoming version of the popular programming language, brings several updates and improvements to its preview features. Preview features are experimental language and API features that are introduced in one release to gather user feedback before being finalized in a future release.

In this blog post, we will explore some of the updates made to preview features in Java 18.

## 1. Pattern Matching for instanceof

One of the preview features introduced in Java 14 was pattern matching for instanceof. This feature allows developers to simplify the code when checking types and extracting information from objects.

In Java 18, pattern matching for instanceof has received some enhancements. Now, developers can use pattern matching in switch statements with instanceof conditions. This enables more concise and expressive code when working with conditional behavior based on object types.

Here's an example that demonstrates the use of pattern matching for instanceof in a switch statement:

```java
public void process(Object obj) {
    switch (obj) {
        case String s -> System.out.println("String: " + s);
        case Integer i -> System.out.println("Integer: " + i);
        default -> System.out.println("Unknown type");
    }
}
```

This enhancement simplifies the code and reduces the boilerplate needed for type checks.

## 2. Sealed Classes

Sealed classes, which were introduced as a preview feature in Java 15, provide control over inheritance and restrict the number of subclasses that can extend a certain class or interface.

In Java 18, sealed classes have undergone improvements. Now, it is possible to declare a class or interface sealed without explicitly specifying the permitted subclasses. This allows future proofing the sealed hierarchy, making it easier to add or remove subclasses without modifying the sealed class.

Here's an example of declaring a sealed class without specifying the permitted subclasses:

```java
public sealed class Shape permits Circle, Rectangle, Triangle {
    // class definition
}
```

This enhancement simplifies the sealed class declaration and provides more flexibility when managing the subclasses.

## Conclusion

Java 18 brings exciting updates to its preview features, enhancing the overall programming experience for developers. The enhancements to pattern matching for instanceof and sealed classes provide more expressive and flexible ways of working with types and inheritance.

We encourage Java developers to explore these preview features and provide feedback to help shape the future of Java. Stay tuned for more updates on Java 18 and its final release.

#References
- [Oracle Java Documentation](https://docs.oracle.com/en/java/javase/18/)