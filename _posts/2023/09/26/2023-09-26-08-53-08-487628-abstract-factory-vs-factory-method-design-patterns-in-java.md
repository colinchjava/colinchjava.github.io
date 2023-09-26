---
layout: post
title: "Abstract factory vs. factory method design patterns in Java"
description: " "
date: 2023-09-26
tags: [AbstractFactory, FactoryMethod]
comments: true
share: true
---

When it comes to software design patterns, two commonly used ones are the Abstract Factory and Factory Method patterns. Both patterns involve creating objects, but they serve different purposes. In this article, we will explore the differences between these two design patterns and when to use each one.

## Abstract Factory Pattern

The Abstract Factory pattern is a creational design pattern that provides an interface for creating families of related or dependent objects without specifying their concrete classes. It allows you to create objects without specifying their exact types, which promotes loose coupling and scalability.

The key components of the Abstract Factory pattern are:

1. *AbstractFactory*: This is the interface that declares the creation methods for different types of objects.
2. *ConcreteFactories*: These are the classes that implement the AbstractFactory interface and are responsible for creating specific types of objects.
3. *AbstractProduct*: This is the interface that declares the common methods that the product classes will implement.
4. *ConcreteProducts*: These are the classes that implement the AbstractProduct interface and represent the different types of products that can be created.

To use the Abstract Factory pattern in Java, you would define the abstract factory, concrete factories, abstract products, and concrete products. Then you would instantiate the concrete factory and use it to create the desired objects.

```java
public interface AbstractFactory {
    Product createProduct();
}

public class ConcreteFactory1 implements AbstractFactory {
    @Override
    public Product createProduct() {
        return new ConcreteProduct1();
    }
}

public class ConcreteFactory2 implements AbstractFactory {
    @Override
    public Product createProduct() {
        return new ConcreteProduct2();
    }
}

public interface Product {
    void performAction();
}

public class ConcreteProduct1 implements Product {
    @Override
    public void performAction() {
        // Implementation for ConcreteProduct1
        System.out.println("Performing action in ConcreteProduct1");
    }
}

public class ConcreteProduct2 implements Product {
    @Override
    public void performAction() {
        // Implementation for ConcreteProduct2
        System.out.println("Performing action in ConcreteProduct2");
    }
}

// Usage
AbstractFactory factory = new ConcreteFactory1();
Product product = factory.createProduct();
product.performAction();
```

## Factory Method Pattern

The Factory Method pattern is also a creational design pattern, but it focuses on providing a method for creating objects in a superclass, while allowing subclasses to alter the type of objects that will be created. This pattern is useful when you have multiple subclasses with different implementations, and you want to delegate the object creation to the subclasses.

The key components of the Factory Method pattern are:

1. *Creator*: This is the superclass or interface that declares the factory method for creating products.
2. *ConcreteCreators*: These are the subclasses that implement or extend the Creator and override the factory method to create specific types of products.
3. *Product*: This is the interface or superclass that declares the common methods that the product classes will implement.
4. *ConcreteProducts*: These are the classes that implement or extend the Product interface and represent the different types of products that can be created.

To use the Factory Method pattern in Java, you would define the creator, concrete creators, product, and concrete products. Then you would instantiate the concrete creator and use it to create the desired objects.

```java
public abstract class Creator {
    public abstract Product createProduct();
    
    public void performAction() {
        Product product = createProduct();
        product.performAction();
    }
}

public class ConcreteCreator1 extends Creator {
    @Override
    public Product createProduct() {
        return new ConcreteProduct1();
    }
}

public class ConcreteCreator2 extends Creator {
    @Override
    public Product createProduct() {
        return new ConcreteProduct2();
    }
}

public interface Product {
    void performAction();
}

public class ConcreteProduct1 implements Product {
    @Override
    public void performAction() {
        // Implementation for ConcreteProduct1
        System.out.println("Performing action in ConcreteProduct1");
    }
}

public class ConcreteProduct2 implements Product {
    @Override
    public void performAction() {
        // Implementation for ConcreteProduct2
        System.out.println("Performing action in ConcreteProduct2");
    }
}

// Usage
Creator creator = new ConcreteCreator1();
creator.performAction();
```

## When to Use Each Design Pattern

Now that we have explained both the Abstract Factory and Factory Method patterns, let's discuss when to use each pattern:

- Use the **Abstract Factory** pattern when:

  - You need to create families of related or dependent objects.
  - You want to provide a single interface for creating multiple types of objects.
  - You want to isolate concrete implementation classes from the client code.

- Use the **Factory Method** pattern when:

  - You have a superclass that cannot anticipate the type of objects its subclasses will create.
  - You want to delegate the responsibility of object creation to subclasses.
  - You want to provide a framework for creating multiple types of objects.

In summary, the Abstract Factory and Factory Method patterns are both useful for creating objects, but they differ in their approach. Choose the pattern that best suits your needs based on the requirements of your project. 

Hashtags: #AbstractFactory #FactoryMethod