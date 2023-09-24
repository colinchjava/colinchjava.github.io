---
layout: post
title: "Test doubles in Java unit testing: fakes, mocks, spies"
description: " "
date: 2023-09-24
tags: [Java, UnitTesting]
comments: true
share: true
---

Unit testing is a crucial part of the software development process. It helps us ensure the quality and reliability of our code by testing each component in isolation. However, unit testing often requires interacting with external dependencies such as databases, APIs, or third-party services. These dependencies can make unit tests slow, unreliable, and difficult to maintain.

To address this problem, we use test doubles - objects that replace the real dependencies during testing. In Java unit testing, there are three common types of test doubles: fakes, mocks, and spies. Let's explore each of them in detail.

## 1. Fakes

Fakes are simple, lightweight implementations of the external dependencies. They provide the necessary functionality required for the test, but they usually don't implement the complete behavior of the real dependency. Fakes are especially useful when testing database integrations or network communication.

Example code:

```java
public class FakeDatabase implements Database {
    private Map<String, String> data = new HashMap<>();

    @Override
    public String get(String key) {
        return data.get(key);
    }

    @Override
    public void put(String key, String value) {
        data.put(key, value);
    }
}
```

In the above code, `FakeDatabase` implements the `Database` interface, providing a simple in-memory map to store key-value pairs. This fake implementation allows us to test code that interacts with the database without the need for a real database.

## 2. Mocks

Mocks are more sophisticated test doubles that record the interactions between the tested code and the dependency. They allow us to define expected behaviors and verify that the interactions happen as expected. Mocking frameworks like Mockito or EasyMock make it easier to create and manage mocks in Java.

Example code using Mockito:

```java
public interface EmailService {
    void sendEmail(String to, String subject, String body);
}

@Test
public void testSendNotificationEmail() {
    EmailService emailServiceMock = Mockito.mock(EmailService.class);
    User user = new User("John Doe");
    NotificationService notificationService = new NotificationService(emailServiceMock);

    notificationService.sendNotificationEmail(user);

    Mockito.verify(emailServiceMock).sendEmail(Mockito.eq(user.getEmail()), Mockito.anyString(), Mockito.anyString());
}
```

In the code snippet above, we create a mock `EmailService` using Mockito. We define the expected behavior of the `sendEmail` method and then verify that it was called with the specified arguments during the test.

## 3. Spies

Spies are similar to mocks but allow us to record the interactions while still using the real dependency. They can be useful when we want to partially mock an object, that is, replace only certain methods while keeping the rest of the behavior intact. Spies are commonly used in situations where modifying the original code to inject dependencies is not possible or desirable.

Example code using Mockito:

```java
@Test
public void testUpdateUserBalance() {
    User user = new User("John Doe");
    user.setBalance(100);
    UserRepository userRepository = new UserRepository();
    UserRepository userRepositorySpy = Mockito.spy(userRepository);
    UserService userService = new UserService(userRepositorySpy);

    userService.updateUserBalance(user, 50);

    Mockito.verify(userRepositorySpy).saveUser(Mockito.eq(user));
    Assert.assertEquals(150, user.getBalance());
}
```

In the code snippet above, we create a spy `UserRepository` using Mockito. We verify that the `saveUser` method was called during the test and assert on the updated user balance.

Using test doubles like fakes, mocks, and spies allows us to write effective unit tests that are fast, reliable, and isolated from external dependencies. By choosing the appropriate test double for each scenario, we can ensure thorough testing of our code while maintaining a good balance between realism and simplicity.

#Java #UnitTesting