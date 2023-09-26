---
layout: post
title: "Overloading of nested classes with different access modifiers in Java"
description: " "
date: 2023-09-26
tags: [Java, NestedClasses]
comments: true
share: true
---

In Java, it is possible to define nested classes within other classes. These nested classes can have different access modifiers such as public, private, or protected. One interesting feature of nested classes is that they can be overloaded, just like regular methods.

Overloading refers to the ability of a class to have multiple methods with the same name but different parameters. This allows us to define different behaviors for the same method name based on the types and number of parameters passed.

To overload a nested class, we follow a similar syntax as we do for regular methods. Let's consider an example where we have a class called `Outer` and inside it, we define a nested class called `Inner`.

```java
public class Outer {
    
    private class Inner {
        public void display() {
            System.out.println("Private Inner Class");
        }
    }
    
    public class Inner {
        public void display() {
            System.out.println("Public Inner Class");
        }
    }
    
    protected class Inner {
        public void display() {
            System.out.println("Protected Inner Class");
        }
    }
}
```

In the above code snippet, we have defined three versions of the nested class `Inner`, each with a different access modifier: private, public, and protected.

To use these overloaded nested classes, we can create objects of the respective classes and invoke the `display()` method.

```java
public class Main {
    
    public static void main(String[] args) {
        
        Outer outer = new Outer();
        
        Outer.PrivateInner privateInner = outer.new PrivateInner();
        privateInner.display();
        
        Outer.PublicInner publicInner = outer.new PublicInner();
        publicInner.display();
        
        Outer.ProtectedInner protectedInner = outer.new ProtectedInner();
        protectedInner.display();
    }
}
```

In the above code, we create objects of the `Outer`, `PrivateInner`, `PublicInner`, and `ProtectedInner` classes and invoke the `display()` method on each. This will output the respective messages defined in each version of the nested class.

By overloading nested classes with different access modifiers, we can define different behaviors and encapsulate functionality based on the intended visibility and usage.

## Conclusion

In Java, it is possible to overload nested classes with different access modifiers. This allows us to define different behaviors for the same nested class name based on the access modifier used. Overloading nested classes can help in encapsulating functionality and controlling visibility. With the knowledge of nested class overloading, you can enhance the readability and maintainability of your Java code. #Java #NestedClasses