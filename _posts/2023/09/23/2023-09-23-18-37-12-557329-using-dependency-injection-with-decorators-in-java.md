---
layout: post
title: "Using Dependency Injection with decorators in Java."
description: " "
date: 2023-09-23
tags: [Java, DependencyInjection]
comments: true
share: true
---

Dependency Injection (DI) is a design pattern used to implement loose coupling between classes and their dependencies. It allows us to inject dependencies into a class rather than having the class create or manage its own dependencies. Decorators, on the other hand, are design patterns used to dynamically add functionality to an object at runtime.

In Java, we can combine both DI and decorators to enhance the modularity and flexibility of our code. Let's see how we can achieve this using some example code.

## Step 1: Define the interfaces

First, we need to define the interfaces for the component and decorator classes. This allows us to define the contract that each class must adhere to. For example:

```java
public interface Component {
    void operation();
}

public interface Decorator extends Component {
    // Additional methods or properties for the decorator
}
```

## Step 2: Implement the component class

Next, we implement the component class that provides the base functionality. This class will be decorated by other classes. For example:

```java
public class ConcreteComponent implements Component {
    public void operation() {
        System.out.println("Performing operation.");
    }
}
```

## Step 3: Implement the decorator classes

Now, we can implement the decorator classes that add functionality to our component. These classes should implement the `Decorator` interface and also have a reference to the `Component`. For example:

```java
public class DecoratorA implements Decorator {
    private Component component;

    public DecoratorA(Component component) {
        this.component = component;
    }

    public void operation() {
        System.out.println("Decorator A: Before operation.");
        component.operation();
        System.out.println("Decorator A: After operation.");
    }
}

public class DecoratorB implements Decorator {
    private Component component;

    public DecoratorB(Component component) {
        this.component = component;
    }

    public void operation() {
        System.out.println("Decorator B: Before operation.");
        component.operation();
        System.out.println("Decorator B: After operation.");
    }
}
```

## Step 4: Configure the dependency injection

Finally, we configure the dependency injection framework (such as Spring or Guice) to inject the dependencies and wire everything together. For example, using Spring:

```java
@Configuration
public class AppConfig {
    @Bean
    public Component component() {
        return new ConcreteComponent();
    }

    @Bean
    public DecoratorA decoratorA(Component component) {
        return new DecoratorA(component);
    }

    @Bean
    public DecoratorB decoratorB(Component component) {
        return new DecoratorB(component);
    }
}

public class Main {
    public static void main(String[] args) {
        ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        DecoratorA decoratorA = context.getBean(DecoratorA.class);
        decoratorA.operation();

        DecoratorB decoratorB = context.getBean(DecoratorB.class);
        decoratorB.operation();
    }
}
```

By using dependency injection, we can easily swap out different decorators or components without modifying the client code.

Using decorators with dependency injection allows us to dynamically add functionality to classes and achieve a high level of flexibility and modularity in our code.

#Java #DependencyInjection #Decorators