---
layout: post
title: "RabbitMQ message routing in Java"
description: " "
date: 2023-09-18
tags: [rabbitmq, messagerouting]
comments: true
share: true
---

RabbitMQ is a popular open-source message broker that allows applications to communicate with each other by sending and receiving messages. One of the key features of RabbitMQ is its flexible message routing capability, which allows messages to be directed to specific queues based on routing criteria. In this blog post, we will explore how to implement message routing using RabbitMQ in Java.

## Setting up RabbitMQ

Before we proceed with message routing, let's first set up RabbitMQ on our local system. You can download and install RabbitMQ from the official website or use a Docker container for convenience.

Once RabbitMQ is installed, start the RabbitMQ server and make sure it is up and running.

## Creating Queues and Exchanges

In RabbitMQ, messages are sent to exchanges and then routed to queues based on routing criteria. Therefore, we need to create exchanges and queues before we can start routing messages.

```java
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.Channel;

public class RabbitMQSetup {
    private static final String EXCHANGE_NAME = "message_exchange";
    private static final String QUEUE_NAME = "message_queue";
    
    public static void main(String[] args) {
        try {
            ConnectionFactory factory = new ConnectionFactory();
            factory.setHost("localhost");
            Connection connection = factory.newConnection();
            Channel channel = connection.createChannel();
            
            // Create a direct exchange
            channel.exchangeDeclare(EXCHANGE_NAME, "direct");
            
            // Create a queue
            channel.queueDeclare(QUEUE_NAME, false, false, false, null);
            
            // Bind the queue to the exchange with a routing key
            String routingKey = "message_routing_key";
            channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, routingKey);
            
            System.out.println("Setup completed!");
            
            channel.close();
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

In the code above, we are creating a direct exchange named "message_exchange" and a queue named "message_queue". We then bind the queue to the exchange using a routing key "message_routing_key". This means that any message with the routing key "message_routing_key" will be routed to the "message_queue".

## Sending and Receiving Messages

Once we have the queues and exchanges set up, we can start sending and receiving messages with routing.

### Sending Messages

```java
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.Channel;

public class MessageSender {
    private static final String EXCHANGE_NAME = "message_exchange";
    private static final String ROUTING_KEY = "message_routing_key";
    
    public static void main(String[] args) {
        try {
            ConnectionFactory factory = new ConnectionFactory();
            factory.setHost("localhost");
            Connection connection = factory.newConnection();
            Channel channel = connection.createChannel();
            
            String message = "Hello, RabbitMQ!";
            
            // Publish the message to the exchange with the routing key
            channel.basicPublish(EXCHANGE_NAME, ROUTING_KEY, null, message.getBytes());
            
            System.out.println("Message sent: " + message);
            
            channel.close();
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

In the code above, we are publishing a message to the exchange with the specified routing key "message_routing_key". This message will be routed to the queue we set up earlier.

### Receiving Messages

```java
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.DefaultConsumer;
import com.rabbitmq.client.Envelope;

public class MessageReceiver {
    private static final String QUEUE_NAME = "message_queue";
    
    public static void main(String[] args) {
        try {
            ConnectionFactory factory = new ConnectionFactory();
            factory.setHost("localhost");
            Connection connection = factory.newConnection();
            Channel channel = connection.createChannel();
            
            // Consume messages from the queue
            channel.basicConsume(QUEUE_NAME, true, new DefaultConsumer(channel) {
                @Override
                public void handleDelivery(String consumerTag, Envelope envelope, com.rabbitmq.client.AMQP.BasicProperties properties, byte[] body) {
                    String message = new String(body, "UTF-8");
                    System.out.println("Message received: " + message);
                }
            });
            
            System.out.println("Waiting for messages...");
            
            // Keep the application running to receive messages
            Thread.sleep(5000);
            
            channel.close();
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

In the code above, we are consuming messages from the queue "message_queue" using a `DefaultConsumer`. Whenever a message is received, the `handleDelivery` method is invoked, and we can process the received message.

## Conclusion

In this blog post, we have learned how to implement message routing using RabbitMQ in Java. We have seen how to set up exchanges, queues, and bindings, as well as how to send and receive messages with routing. Message routing is a powerful feature of RabbitMQ that enables efficient and flexible message delivery in distributed systems.

#rabbitmq #messagerouting