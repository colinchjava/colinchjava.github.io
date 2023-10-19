---
layout: post
title: "Working with Android runtime bytecode transformation using ASM Library"
description: " "
date: 2023-10-20
tags: [AndroidDevelopment, BytecodeTransformation]
comments: true
share: true
---

In the world of Android development, there are times when we need to dynamically modify the bytecode of a class at runtime. This can be useful for various purposes such as adding/logging method calls, intercepting network requests, or even injecting custom functionality into third-party libraries.

One popular library for working with bytecode manipulation is ASM (formerly known as the "Java bytecode Manipulation Framework"). ASM is a powerful and efficient library that provides developers with the ability to read, write, and modify bytecode dynamically.

## What is ASM?

ASM is a Java library used for analyzing and transforming Java bytecode. It provides a simple and lightweight API for bytecode manipulation without requiring an understanding of the internal details of the Java Virtual Machine (JVM). With ASM, it’s possible to dynamically modify classes, add or remove methods, fields, and even change the logic of existing code.

## Why use ASM for Android?

There are several benefits to using ASM for Android bytecode transformation:

1. **Performance**: ASM is highly optimized for performance and has a minimal memory footprint. This makes it ideal for resource-constrained mobile devices like Android.

2. **Flexibility**: ASM provides a rich set of APIs that allow developers to work at a fine-grained level, giving them full control over the bytecode transformation process. This level of control enables developers to implement complex modifications with ease.

3. **Compatibility**: ASM supports different versions of the Java bytecode format, making it compatible with various Android runtime environments.

4. **Maturity**: ASM has been around for many years and is widely adopted in the Java ecosystem. It has a mature and stable codebase, with regular updates and bug fixes.

## Getting Started with ASM

To get started with ASM in an Android project, you need to add the ASM dependency to your project's build.gradle file:

```groovy
dependencies {
    implementation 'org.ow2.asm:asm:9.2'
}
```

Now, let's consider a simple example where we modify the bytecode of an Android class at runtime using ASM. Suppose we have a class `MyClass` with a single method `doSomething()`:

```java
public class MyClass {
    public void doSomething() {
        // Original method code
    }
}
```

We want to inject a log statement at the beginning of the `doSomething()` method. Here's how you can achieve this using ASM:

```java
import org.objectweb.asm.*;

public class MyClassTransformer {
    public byte[] transform(byte[] classBytes) {
        ClassReader classReader = new ClassReader(classBytes);
        ClassWriter classWriter = new ClassWriter(classReader, ClassWriter.COMPUTE_MAXS);

        ClassVisitor classVisitor = new ClassVisitor(Opcodes.ASM9, classWriter) {
            @Override
            public MethodVisitor visitMethod(int access, String name, String descriptor, String signature, String[] exceptions) {
                MethodVisitor methodVisitor = super.visitMethod(access, name, descriptor, signature, exceptions);

                if (name.equals("doSomething")) {
                    return new MethodVisitor(Opcodes.ASM9, methodVisitor) {
                        @Override
                        public void visitCode() {
                            super.visitCode();
                            visitFieldInsn(Opcodes.GETSTATIC, "java/lang/System", "out", "Ljava/io/PrintStream;");
                            visitLdcInsn("Method called: MyClass.doSomething()");
                            visitMethodInsn(Opcodes.INVOKEVIRTUAL, "java/io/PrintStream", "println", "(Ljava/lang/String;)V", false);
                        }
                    };
                }

                return methodVisitor;
            }
        };

        classReader.accept(classVisitor, 0);
        return classWriter.toByteArray();
    }
}
```

In this example, we define a `MyClassTransformer` class responsible for transforming the bytecode of `MyClass`. The `transform()` method takes the original class bytecode as input and returns the modified bytecode.

We use `ClassReader` to read the original class bytecode and `ClassWriter` to write the modified bytecode. The `ClassVisitor` and `MethodVisitor` classes allow us to visit class and method instructions.

In the `visitMethod()` method of the `ClassVisitor`, we check if the method being visited is `doSomething()`. If it is, we create a `MethodVisitor` to visit the instructions of the method. In this case, we add bytecode instructions to print a log statement using `System.out.println()`.

## Applying the Transformation

To apply the bytecode transformation, you need to load the original class, transform the bytecode using the `MyClassTransformer`, and redefine the class using reflection:

```java
public class ExampleActivity extends AppCompatActivity {
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);

        try {
            Class<?> originalClass = MyClass.class;
            byte[] transformedBytes = new MyClassTransformer().transform(readBytesFromAsset("MyClass.class"));

            // Define the transformed class
            Class<?> transformedClass = defineClass(originalClass.getName(), transformedBytes);

            // Optionally, you can instantiate an instance of the transformed class
            Object instance = transformedClass.getDeclaredConstructor().newInstance();

            // Invoke the modified method
            Method method = transformedClass.getMethod("doSomething");
            method.invoke(instance);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    private byte[] readBytesFromAsset(String path) throws IOException {
        InputStream input = getAssets().open(path);
        ByteArrayOutputStream output = new ByteArrayOutputStream();

        byte[] buffer = new byte[4096];
        int bytesRead;
        while ((bytesRead = input.read(buffer)) != -1) {
            output.write(buffer, 0, bytesRead);
        }

        return output.toByteArray();
    }

    private Class<?> defineClass(String className, byte[] classBytes) {
        ClassLoader classLoader = getClassLoader();
        Method defineClassMethod;

        try {
            defineClassMethod = ClassLoader.class.getDeclaredMethod("defineClass",
                    String.class, byte[].class, int.class, int.class);
            defineClassMethod.setAccessible(true);
        } catch (NoSuchMethodException e) {
            throw new RuntimeException("Failed to get defineClass() method: " + e.getMessage());
        }

        try {
            return (Class<?>) defineClassMethod.invoke(classLoader,
                    className, classBytes, 0, classBytes.length);
        } catch (Exception e) {
            throw new RuntimeException("Failed to define class: " + e.getMessage());
        }
    }
}
```

In the above example, we create an `ExampleActivity` that performs the bytecode transformation. It reads the original `MyClass.class` file from the assets folder, calls the `transform()` method to modify the bytecode, defines the transformed class using reflection, instantiates an instance of the transformed class, and invokes the modified method.

## Conclusion

In this blog post, we explored the ASM library and showcased how to work with Android runtime bytecode transformation using ASM. We learned about the benefits of using ASM, how to get started with it, and how to apply bytecode transformations to Android classes at runtime. ASM provides a powerful and flexible way to modify bytecode, opening up endless possibilities for enhancing and customizing Android applications. For more information, refer to the official ASM documentation and examples.

**#AndroidDevelopment #BytecodeTransformation**