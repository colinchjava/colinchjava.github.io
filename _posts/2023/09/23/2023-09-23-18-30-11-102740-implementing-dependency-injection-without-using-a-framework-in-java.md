---
layout: post
title: "Implementing Dependency Injection without using a framework in Java."
description: " "
date: 2023-09-23
tags: [DependencyInjection]
comments: true
share: true
---

Dependency Injection (DI) is a design pattern used to decouple components and manage their dependencies. While many Java frameworks provide built-in DI support, it is possible to implement DI without relying on any external framework. In this article, we will explore how to implement DI manually in a Java application.

## What is Dependency Injection?

Dependency Injection is based on the principle of Inversion of Control (IoC), which states that the control flow of a program should be inverted. Instead of components creating their dependencies, the dependencies are provided to the components. This makes the components more reusable and testable.

## Manually implementing DI in Java

To implement DI manually, we need to follow these steps:

1. **Identify the dependencies**: Determine the dependencies required by a component.

2. **Create the component interfaces**: Define interfaces to represent the components that will have their dependencies injected. These interfaces will provide a contract for the implementation.

3. **Implement the components**: Implement the component classes that implement the interfaces defined in the previous step.

4. **Create a container**: Create a container class that will manage the creation and injection of dependencies.

5. **Wire the dependencies**: In the container class, create instances of the component classes and inject their dependencies.

6. **Use the components**: Finally, use the components in your application.

Let's see an example to understand how DI can be implemented manually in Java.

```java
public class EmailService implements NotificationService {
    public void sendNotification(String message) {
        // Implementation to send an email
    }
}

public class SMSNotificationService implements NotificationService {
    public void sendNotification(String message) {
        // Implementation to send an SMS
    }
}

public interface NotificationService {
    void sendNotification(String message);
}

public class NotificationAppContainer {
    private NotificationService notificationService;
    
    public NotificationAppContainer() {
        notificationService = new EmailService();
        // Dependency injection
    }
    
    public NotificationService getNotificationService() {
        return notificationService;
    }
}

public class MyApp {
    public static void main(String[] args) {
        NotificationAppContainer container = new NotificationAppContainer();
        
        NotificationService service = container.getNotificationService();
        service.sendNotification("Hello, world!");
    }
}
```

In the above example, we have two implementations of the `NotificationService` interface: `EmailService` and `SMSNotificationService`. The `NotificationAppContainer` class acts as a container and is responsible for creating instances of the dependencies. In this case, it creates an instance of `EmailService` and injects it as a dependency.

By manually wiring the dependencies in the container, we achieve the desired effect of dependency injection without relying on any external framework.

## Conclusion

Implementing Dependency Injection without using a framework in Java requires manually managing the creation and injection of dependencies. By following the steps outlined in this article, you can achieve the benefits of DI in your Java applications. While using a framework may provide more features and convenience, understanding the manual implementation helps you grasp the underlying concepts of DI. #Java #DependencyInjection