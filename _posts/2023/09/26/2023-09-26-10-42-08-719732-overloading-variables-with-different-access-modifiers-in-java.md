---
layout: post
title: "Overloading variables with different access modifiers in Java"
description: " "
date: 2023-09-26
tags: [Java, Variables]
comments: true
share: true
---

In Java, it is possible to overload variables with different access modifiers. Overloading refers to the ability to define multiple methods or variables with the same name but different parameters or different access modifiers.

Let's consider an example to understand how overloading variables with different access modifiers works:

```java
public class ExampleClass {
    public int publicVariable = 10;
    private int privateVariable = 20;
    
    // Overloaded variable with different access modifier
    protected int protectedVariable = 30;
    
    public void printVariables() {
        System.out.println("Public variable: " + publicVariable);
        System.out.println("Private variable: " + privateVariable);
        System.out.println("Protected variable: " + protectedVariable);
    }
    
    // Overloaded method to access private variable
    public void changePrivateVariable(int newValue) {
        privateVariable = newValue;
    }
    
    // Overloaded method to access protected variable
    public void changeProtectedVariable(int newValue) {
        protectedVariable = newValue;
    }
}
```

In the example above, we have a class `ExampleClass` with three variables: `publicVariable`, `privateVariable`, and `protectedVariable`. These variables have different access modifiers assigned to them: `public`, `private`, and `protected`.

The `printVariables()` method is used to print the values of these variables. Notice that we are able to access the `publicVariable` directly, but for the `privateVariable` and `protectedVariable`, we have separate methods `changePrivateVariable()` and `changeProtectedVariable()` respectively to modify their values.

Now, let's create an instance of `ExampleClass` and test the code:

```java
public class Main {
    public static void main(String[] args) {
        ExampleClass example = new ExampleClass();
        example.printVariables();
        
        example.changePrivateVariable(50);
        example.changeProtectedVariable(70);
        
        example.printVariables();
    }
}
```

When we run the above code, the output will be:

```
Public variable: 10
Private variable: 20
Protected variable: 30

Public variable: 10
Private variable: 50
Protected variable: 70
```

As you can see, even though the `privateVariable` and `protectedVariable` have different access modifiers, we can still modify their values using the appropriate methods (`changePrivateVariable()` and `changeProtectedVariable()`).

In summary, overloading variables with different access modifiers in Java allows us to have variables with different visibility and access levels within a class, providing flexibility in how we interact with them.

#Java #Variables