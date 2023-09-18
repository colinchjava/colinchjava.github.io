---
layout: post
title: "RabbitMQ publish-subscribe pattern in Java"
description: " "
date: 2023-09-18
tags: [rabbitmq, java]
comments: true
share: true
---

RabbitMQ is a widely used message broker that allows different applications to communicate with each other using a messaging protocol. It supports various messaging patterns, and one of the most popular ones is the publish-subscribe pattern.

The publish-subscribe pattern allows multiple receivers, also known as subscribers, to receive messages from a single sender, also known as a publisher. This pattern is useful when you want to broadcast messages to a group of subscribers, decoupling the sender from the receivers.

In Java, you can implement the publish-subscribe pattern using the RabbitMQ Java Client library. Here is an example code snippet to demonstrate how to publish and subscribe to messages using RabbitMQ in Java:

```java
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;
import com.rabbitmq.client.AMQP;

import java.io.IOException;

public class RabbitMQExample {

    private static final String EXCHANGE_NAME = "my_exchange";

    public static void main(String[] args) throws Exception {
        // Publish Messages
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");
        Connection connection = factory.newConnection();
        Channel channel = connection.createChannel();

        channel.exchangeDeclare(EXCHANGE_NAME, "fanout"); // Create a fanout exchange

        String message = "Hello RabbitMQ!";
        channel.basicPublish(EXCHANGE_NAME, "", null, message.getBytes());
        System.out.println("Sent message: " + message);

        // Subscribe to Messages
        channel.queueDeclare("my_queue", false, false, false, null);
        channel.queueBind("my_queue", EXCHANGE_NAME, "");

        DefaultConsumer consumer = new DefaultConsumer(channel) {
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
                String message = new String(body, "UTF-8");
                System.out.println("Received message: " + message);
            }
        };

        channel.basicConsume("my_queue", true, consumer);

        // Close the connections
        channel.close();
        connection.close();
    }
}
```

In this example, the code publishes a message with the text "Hello RabbitMQ!" to the specified exchange. The exchange is declared as a "fanout" exchange, which means it will broadcast the message to all queues attached to it.

To subscribe to the messages, a queue is declared and bound to the same exchange. The `DefaultConsumer` class is used to consume the messages from the queue. In this case, the received message is simply printed to the console.

Remember to include the RabbitMQ Java Client library in your project's dependencies to compile and run the code successfully.

#rabbitmq #java