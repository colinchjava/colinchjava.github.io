---
layout: post
title: "Creating event-driven microservices with GlassFish and Eclipse MicroProfile Reactive Messaging in Java"
description: " "
date: 2023-09-17
tags: []
comments: true
share: true
---

In today's world of distributed systems and cloud computing, event-driven architectures have gained popularity due to their scalability, flexibility, and fault-tolerance. Microservices, on the other hand, have become the preferred approach for building modular and independently deployable applications. Combining these two concepts, we can effectively create event-driven microservices that communicate with each other through asynchronous messaging.

## What is Eclipse MicroProfile Reactive Messaging?

**Eclipse MicroProfile Reactive Messaging** is a specification that allows developers to build event-driven applications using microservices. It provides a set of annotations and APIs for sending and receiving messages asynchronously, making it easy to implement messaging patterns such as publish-subscribe, request-reply, and event sourcing.

## Setting up GlassFish and MicroProfile Reactive Messaging

Before we dive into the code, let's set up our development environment. We'll be using GlassFish as our application server and Eclipse MicroProfile Reactive Messaging for message handling.

1. Download and install GlassFish from the [official website](https://javaee.github.io/glassfish/download). Make sure to choose the latest stable release.

2. Create a new Java project in Eclipse or your preferred IDE.

3. Add the required dependencies to your project's `pom.xml` file:
```xml
<dependencies>
    <dependency>
        <groupId>org.eclipse.microprofile.reactive.messaging</groupId>
        <artifactId>microprofile-reactive-messaging-api</artifactId>
        <version>2.1</version>
        <scope>provided</scope>
    </dependency>
</dependencies>
```

4. Configure your GlassFish instance to enable MicroProfile Reactive Messaging.

## Implementing an event-driven microservice

Let's say we have two microservices: `OrderService` and `EmailService`. Whenever a new order is placed in the `OrderService`, it should send an email notification to the customer through the `EmailService`. We'll implement this using MicroProfile Reactive Messaging.

First, let's define the `Order` class to represent an order:
```java
public class Order {
    private String orderId;
    private String customerEmail;
    // Other order fields, getters, and setters
}
```

Next, let's implement the `OrderService` microservice using MicroProfile Reactive Messaging annotations:
```java
@ApplicationScoped
@Incoming("orders")
public class OrderService {
    @Inject
    private Message<String> message;

    @Incoming("orders")
    public void processOrder(Order order) {
        // Process the order logic here
        sendMessageToEmailService(order);
    }

    private void sendMessageToEmailService(Order order) {
        // Convert the order to JSON string
        String jsonOrder = toJson(order);

        // Send the message to the EmailService
        message
            .withPayload(jsonOrder)
            .withHeader("type", "new-order")
            .send();
    }

    private String toJson(Order order) {
        // Convert the object to JSON string using a JSON library
        // Example: use Jackson ObjectMapper
        ObjectMapper objectMapper = new ObjectMapper();
        try {
            return objectMapper.writeValueAsString(order);
        } catch (JsonProcessingException e) {
            e.printStackTrace();
            return null;
        }
    }
}
```

And now, let's implement the `EmailService` microservice that receives messages from the `OrderService` and sends emails:
```java
@ApplicationScoped
@Incoming("orders")
public class EmailService {
    @Incoming("orders")
    public void processOrderMessage(Message<String> message) {
        String jsonOrder = message.getPayload();

        JsonObject orderObj = Json.createReader(new StringReader(jsonOrder)).readObject();

        // Extract the required fields from the JSON object
        String customerEmail = orderObj.getString("customerEmail");
        // Extract other order fields if necessary

        // Send the email logic here
        sendEmail(customerEmail);
    }

    private void sendEmail(String customerEmail) {
        // Actual email sending logic
    }
}
```

Finally, we need to configure the messaging infrastructure in the `META-INF/microprofile-config.properties` file:
```properties
mp.messaging.incoming.orders.connector=smallrye-reactive-messaging
mp.messaging.incoming.orders.topic=orders

mp.messaging.outgoing.orders.connector=smallrye-reactive-messaging
mp.messaging.outgoing.orders.topic=orders
```

## Conclusion

By leveraging the power of GlassFish and Eclipse MicroProfile Reactive Messaging, we can create event-driven microservices in Java. This allows us to build scalable and resilient applications that can handle a large number of events efficiently.