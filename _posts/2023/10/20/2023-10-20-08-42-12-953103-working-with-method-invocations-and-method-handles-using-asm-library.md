---
layout: post
title: "Working with method invocations and method handles using ASM Library"
description: " "
date: 2023-10-20
tags: [bytecode]
comments: true
share: true
---

In this blog post, we will explore how to work with method invocations and method handles using the ASM library in Java. 

Table of Contents:
- [Introduction](#introduction)
- [ASM Library](#asm-library)
- [Method Invocations](#method-invocations)
- [Method Handles](#method-handles)
- [Conclusion](#conclusion)

## Introduction

Method invocations and method handles are important concepts in Java that allow us to dynamically call methods at runtime. The ASM library provides a powerful way to work with bytecode and manipulate method invocations and method handles.

## ASM Library

ASM is a popular Java bytecode manipulation framework that allows us to read, write, and transform bytecode at runtime. It provides a high-level API that simplifies the process of manipulating bytecode.

To get started with ASM, we need to include the ASM library in our project. We can do this by adding the following dependency to our build file:

```xml
<dependency>
    <groupId>org.ow2.asm</groupId>
    <artifactId>asm</artifactId>
    <version>9.2</version>
</dependency>
```

## Method Invocations

Method invocations are used to invoke methods dynamically at runtime. We can use ASM to modify and manipulate method invocations in bytecode.

To work with method invocations using ASM, we first need to define a `MethodVisitor` that will visit the bytecode instructions of a method. Within the `MethodVisitor`, we can use the `visitMethodInsn` method to modify or replace method invocations.

Here's an example that demonstrates how to modify a method invocation using ASM:

```java
public class MyClass {
    public static void myMethod(){
        System.out.println("Original method");
    }
}

public class MyMethodVisitor extends MethodVisitor {
    public MyMethodVisitor(int api, MethodVisitor methodVisitor) {
        super(api, methodVisitor);
    }

    @Override
    public void visitMethodInsn(int opcode, String owner, String name, String descriptor, boolean isInterface) {
        if (name.equals("myMethod")) {
            super.visitFieldInsn(opcode, owner, name, descriptor);
            super.visitMethodInsn(opcode, owner, "modifiedMethod", descriptor, isInterface);
        } else {
            super.visitMethodInsn(opcode, owner, name, descriptor, isInterface);
        }
    }
}
```

In the above example, `MyMethodVisitor` extends `MethodVisitor` and overrides the `visitMethodInsn` method. Inside this method, we check if the method being invoked is "myMethod". If it is, we replace the invocation with a new method call to "modifiedMethod".

By using the `MethodVisitor`, we have the flexibility to modify method invocations dynamically in bytecode.

## Method Handles

Method handles are another way to invoke methods dynamically at runtime. They provide a flexible and efficient way to perform method invocations.

With ASM, we can manipulate method handles by accessing the constant pool and bytecode instructions of a class.

Here's an example that demonstrates how to create and manipulate method handles using ASM:

```java
public class MyClass {
    public static void myMethod(String message){
        System.out.println(message);
    }
}

public class MyMethodHandleVisitor extends ClassVisitor {
    public MyMethodHandleVisitor(int api, ClassVisitor classVisitor) {
        super(api, classVisitor);
    }

    @Override
    public MethodVisitor visitMethod(int access, String name, String descriptor, String signature, String[] exceptions) {
        MethodVisitor methodVisitor = super.visitMethod(access, name, descriptor, signature, exceptions);

        if (name.equals("myMethod")) {
            return new MyMethodHandleMethodVisitor(api, methodVisitor);
        }

        return methodVisitor;
    }
}

public class MyMethodHandleMethodVisitor extends MethodVisitor {
    public MyMethodHandleMethodVisitor(int api, MethodVisitor methodVisitor) {
        super(api, methodVisitor);
    }

    @Override
    public void visitCode() {
        super.visitCode();
        super.visitFieldInsn(GETSTATIC, "java/lang/invoke/MethodHandles$Lookup", "PUBLIC", "Ljava/lang/invoke/MethodHandles$Lookup;");

        super.visitLdcInsn(Type.getType("LMyClass;"));
        super.visitLdcInsn("myMethod");

        super.visitMethodInsn(INVOKEVIRTUAL, "java/lang/invoke/MethodHandles$Lookup",
                "findStatic",
                "(Ljava/lang/Class;Ljava/lang/String;Ljava/lang/invoke/MethodType;)Ljava/lang/invoke/MethodHandle;", false);

        super.visitVarInsn(ASTORE, 1);

        super.visitVarInsn(ALOAD, 1);
        super.visitInsn(ICONST_1);
        super.visitLdcInsn("Modified Method");

        super.visitMethodInsn(INVOKEVIRTUAL, "java/lang/invoke/MethodHandle", "invokeExact", "(ILjava/lang/String;)V", false);
    }
}
```

In the above example, `MyMethodHandleVisitor` extends `ClassVisitor` and overrides the `visitMethod` method. Inside this method, we check if the method being visited is "myMethod". If it is, we return a new instance of `MyMethodHandleMethodVisitor`, which extends `MethodVisitor`. In `MyMethodHandleMethodVisitor`, we can manipulate the bytecode to create and modify method handles.

By using ASM, we can manipulate method handles and customize the way methods are invoked dynamically at runtime.

## Conclusion

In this post, we learned how to work with method invocations and method handles using the ASM library in Java. We explored how to modify method invocations dynamically using `MethodVisitor` and how to create and manipulate method handles using `ClassVisitor`. By leveraging ASM's bytecode manipulation capabilities, we have the flexibility to work with method invocations and method handles in our Java applications.

References:
- [ASM website](https://asm.ow2.io/)
- [ASM GitHub repository](https://github.com/ow2-asm/asm)
- [Java Bytecode Manipulation with ASM](https://www.baeldung.com/java-bytecode-manipulation-with-asm) #java #bytecode