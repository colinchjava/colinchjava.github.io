---
layout: post
title: "RabbitMQ topic-based routing in Java"
description: " "
date: 2023-09-18
tags: [staytuned]
comments: true
share: true
---

In distributed systems, message routing plays a crucial role in ensuring efficient and reliable communication between different components. RabbitMQ, a popular message broker, provides flexible routing options to publish and subscribe to messages. One of these options is topic-based routing, which allows messages to be selectively routed based on matching routing keys.

In this blog post, we will explore how to perform topic-based routing using RabbitMQ in Java.

## Prerequisites
To follow along with this tutorial, you will need the following:

- RabbitMQ installed and running
- Java Development Kit (JDK) installed on your machine
- A basic understanding of RabbitMQ concepts like exchanges, queues, and bindings

## Setting Up RabbitMQ
Before we dive into the code, let's quickly set up RabbitMQ. You can download and install RabbitMQ from the official website or use Docker to run it as a container.

Once RabbitMQ is up and running, you need to create a topic exchange to which publishers can send messages and subscribers can bind their queues. You can do this using the RabbitMQ management UI or programmatically using a library like RabbitMQ Java client.

## Creating a Publisher
Let's start by creating a Java class representing our message publisher:

```java
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

public class TopicPublisher {
    private static final String EXCHANGE_NAME = "topic_exchange";
    private static final String ROUTING_KEY = "news.sports";

    public static void main(String[] args) throws IOException, TimeoutException {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");

        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {
            channel.exchangeDeclare(EXCHANGE_NAME, BuiltinExchangeType.TOPIC);

            String message = "New sports news!";
            channel.basicPublish(EXCHANGE_NAME, ROUTING_KEY, null, message.getBytes());
            System.out.println("Published message: " + message);
        }
    }
}
```

In the above code, we create a connection to RabbitMQ, declare a topic exchange, and publish a message with a specific routing key. In this example, we use the routing key "news.sports" to indicate that this message should be routed to subscribers interested in sports news.

## Creating a Subscriber
Now, let's create a Java class representing our message subscriber:

```java
import com.rabbitmq.client.*;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

public class TopicSubscriber {
    private static final String EXCHANGE_NAME = "topic_exchange";
    private static final String BINDING_KEY = "news.*";
    
    public static void main(String[] args) throws IOException, TimeoutException {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");

        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {
            channel.exchangeDeclare(EXCHANGE_NAME, BuiltinExchangeType.TOPIC);

            String queueName = channel.queueDeclare().getQueue();
            channel.queueBind(queueName, EXCHANGE_NAME, BINDING_KEY);

            Consumer consumer = new DefaultConsumer(channel) {
                @Override
                public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
                    String message = new String(body, "UTF-8");
                    System.out.println("Received message: " + message);
                }
            };

            channel.basicConsume(queueName, true, consumer);
        }
    }
}
```

In the above code, we create a connection to RabbitMQ, declare a topic exchange, and bind a queue to the exchange using a binding key. The binding key "news.*" indicates that this subscriber is interested in any news-related messages.

When a message is received, the `handleDelivery` method of the `DefaultConsumer` implementation is invoked, and we print the received message to the console.

## Running the Example
To run the example, ensure that RabbitMQ is running. Compile both the `TopicPublisher` and `TopicSubscriber` classes and run them in separate terminal windows. You should see the publisher successfully publishing a message and the subscriber receiving and printing the message.

## Conclusion
In this tutorial, we explored RabbitMQ's topic-based routing feature and implemented a basic publisher and subscriber in Java. Topic-based routing provides a powerful way to selectively route messages based on routing keys, enabling more fine-grained control over your message flow in distributed systems.

Remember to [**#staytuned**] for more exciting tutorials on RabbitMQ and other messaging technologies.