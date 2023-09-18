---
layout: post
title: "RabbitMQ integration with Apache TomEE in Java"
description: " "
date: 2023-09-18
tags: [RabbitMQ, TomEE]
comments: true
share: true
---

Apache TomEE is a lightweight Java EE application server that provides a robust environment for deploying and running Java web applications. RabbitMQ, on the other hand, is a reliable and scalable message broker that enables systems to communicate asynchronously.

Integrating RabbitMQ with Apache TomEE allows developers to build distributed and decoupled systems, where different components can communicate through messages using the publish-subscribe pattern. In this blog post, we will explore how to integrate RabbitMQ with Apache TomEE in a Java application.

## Prerequisites

Before we get started, make sure you have the following prerequisites installed:

- Apache TomEE (version X.X.X)
- RabbitMQ server (version X.X.X)
- Java Development Kit (JDK) (version X.X)

## Adding Dependencies

To integrate RabbitMQ with Apache TomEE, we need to add the necessary dependencies to our Java project. 

First, add the RabbitMQ Java client library to your project by including the following Maven dependency in your `pom.xml` file:

```xml
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>X.X.X</version>
</dependency>
```

Next, we need to add the TomEE Resource Adapter for JMS (Java Message Service). You can download the resource adapter from the official Apache TomEE website and include it in your TomEE installation directory.

## Configuring RabbitMQ Connection

Once the dependencies are added, we need to configure the connection to the RabbitMQ broker. Create a new class named `RabbitMQConfig` and add the following code:

```java
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;

public class RabbitMQConfig {

    private static final String RABBITMQ_HOST = "localhost";
    private static final int RABBITMQ_PORT = 5672;
    private static final String RABBITMQ_USERNAME = "guest";
    private static final String RABBITMQ_PASSWORD = "guest";
    private static final String RABBITMQ_QUEUE_NAME = "my_queue";

    public static Connection createConnection() throws Exception {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost(RABBITMQ_HOST);
        factory.setPort(RABBITMQ_PORT);
        factory.setUsername(RABBITMQ_USERNAME);
        factory.setPassword(RABBITMQ_PASSWORD);
        return factory.newConnection();
    }

    public static String getQueueName() {
        return RABBITMQ_QUEUE_NAME;
    }
}
```

Update the `RABBITMQ_HOST`, `RABBITMQ_PORT`, `RABBITMQ_USERNAME`, `RABBITMQ_PASSWORD`, and `RABBITMQ_QUEUE_NAME` variables with your RabbitMQ broker information.

## Sending Messages

To send messages to RabbitMQ from Apache TomEE, we need to create a `MessageProducer` and send messages to a specific queue. Here's an example code snippet:

```java
import javax.annotation.Resource;
import javax.inject.Inject;
import javax.jms.Connection;
import javax.jms.MessageProducer;
import javax.jms.Session;
import javax.jms.TextMessage;

public class RabbitMQMessageSender {

    @Inject
    private Connection jmsConnection;

    @Resource
    private Queue rabbitMQQueue;

    public void sendMessage(String message) throws Exception {
        try (Session session = jmsConnection.createSession(false, Session.AUTO_ACKNOWLEDGE)) {
            MessageProducer producer = session.createProducer(rabbitMQQueue);
            TextMessage textMessage = session.createTextMessage(message);
            producer.send(textMessage);
        }
    }
}
```

In this example, we inject the JMS connection and retrieve the RabbitMQ queue from the resource adapter. Then, we create a session, a message producer, and send a text message to the queue.

## Receiving Messages

To receive messages from RabbitMQ in Apache TomEE, we need to create a `MessageListener` and register it with the RabbitMQ queue. Here's an example code snippet:

```java
import javax.annotation.Resource;
import javax.inject.Inject;
import javax.jms.Connection;
import javax.jms.MessageConsumer;
import javax.jms.Session;
import javax.jms.TextMessage;

public class RabbitMQMessageReceiver {

    @Inject
    private Connection jmsConnection;

    @Resource
    private Queue rabbitMQQueue;

    public void receiveMessage() throws Exception {
        try (Session session = jmsConnection.createSession(false, Session.AUTO_ACKNOWLEDGE)) {
            MessageConsumer consumer = session.createConsumer(rabbitMQQueue);
            consumer.setMessageListener(message -> {
                try {
                    if (message instanceof TextMessage) {
                        TextMessage textMessage = (TextMessage) message;
                        System.out.println("Received message: " + textMessage.getText());
                    }
                } catch (Exception e) {
                    e.printStackTrace();
                }
            });
        }
    }
}
```

In this example, we create a message consumer and register a message listener to process incoming messages. We print the received message to the console for demonstration purposes.

## Conclusion

Integrating RabbitMQ with Apache TomEE in Java applications enables reliable and scalable messaging between different components. By following the steps mentioned in this blog post, you can easily integrate RabbitMQ with Apache TomEE and build distributed systems efficiently.

#RabbitMQ #TomEE #Java #Messaging