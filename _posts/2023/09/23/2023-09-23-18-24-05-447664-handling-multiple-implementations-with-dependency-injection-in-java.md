---
layout: post
title: "Handling multiple implementations with Dependency Injection in Java."
description: " "
date: 2023-09-23
tags: [Java, DependencyInjection]
comments: true
share: true
---

Dependency Injection (DI) is a popular design pattern in Java that promotes loose coupling and modularity in software applications. With DI, the responsibility of creating and managing dependencies is delegated to an external entity called the "dependency injector". This not only helps in writing testable code but also allows for easily swapping out implementations without changing the code that uses them.

In some cases, you may have multiple implementations of an interface or an abstract class, and you need a way to handle them dynamically in your application. Fortunately, DI frameworks like Spring and Guice provide elegant solutions to manage multiple implementations.

## Spring Framework

In Spring, you can handle multiple implementations by using the `@Qualifier` annotation along with the `@Autowired` annotation. The `@Qualifier` annotation is used to specify which implementation should be injected when multiple beans of the same type are available.

```java
public interface PaymentService {
    void processPayment();
}

@Service
@Qualifier("creditCard")
public class CreditCardPaymentService implements PaymentService {
    // Implementation goes here
}

@Service
@Qualifier("paypal")
public class PaypalPaymentService implements PaymentService {
    // Implementation goes here
}

@Component
public class PaymentProcessor {

    @Autowired
    @Qualifier("creditCard")
    private PaymentService paymentService;

    // Rest of the code
}
```

In the example above, we have defined two implementation classes of the `PaymentService` interface: `CreditCardPaymentService` and `PaypalPaymentService`. The `@Qualifier` annotation is used to differentiate between them. In the `PaymentProcessor` class, we can inject the desired implementation by using `@Autowired` along with the matching `@Qualifier`.

## Google Guice

In Guice, you can handle multiple implementations by using the `@Named` annotation. The `@Named` annotation is similar to `@Qualifier` in Spring and allows you to provide a name for your implementations.

```java
public interface PaymentService {
    void processPayment();
}

@Singleton
@Named("creditCard")
public class CreditCardPaymentService implements PaymentService {
    // Implementation goes here
}

@Singleton
@Named("paypal")
public class PaypalPaymentService implements PaymentService {
    // Implementation goes here
}

public class PaymentProcessor {

    @Inject
    @Named("creditCard")
    private PaymentService paymentService;

    // Rest of the code
}
```

In the example above, we have marked the implementation classes with `@Named` and provided a unique name for each implementation. In the `PaymentProcessor` class, we can inject the desired implementation by using `@Inject` along with the matching `@Named`.

## Conclusion

Handling multiple implementations with Dependency Injection provides flexibility and maintainability in your Java projects. By leveraging annotations like `@Qualifier` in Spring or `@Named` in Guice, you can easily switch between implementations without making changes to the consuming code. This promotes good software design practices and helps to build modular, testable applications.

#Java #DependencyInjection