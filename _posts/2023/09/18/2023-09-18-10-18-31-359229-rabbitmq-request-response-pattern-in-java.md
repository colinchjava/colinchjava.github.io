---
layout: post
title: "RabbitMQ request-response pattern in Java"
description: " "
date: 2023-09-18
tags: [rabbitmq]
comments: true
share: true
---

RabbitMQ is a popular message broker that allows applications to communicate asynchronously by sending and receiving messages. One of the common messaging patterns used with RabbitMQ is the request-response pattern. In this blog post, we will explore how to implement the request-response pattern in Java using RabbitMQ.

## Setting Up RabbitMQ

Before we dive into the implementation, let's start by setting up RabbitMQ. You can install RabbitMQ locally or use a cloud-based RabbitMQ provider.

Once RabbitMQ is installed, make sure it is running and accessible. You will need the RabbitMQ server URL, username, and password to establish a connection from your Java application.

## Implementing the Request-Response Pattern

To implement the request-response pattern in Java with RabbitMQ, we'll need two components - a sender application and a receiver application.

### Sender Application

The sender application will send a request message to the receiver and wait for the response. Here is an example code snippet:

```java
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.GetResponse;

public class Sender {

    private static final String QUEUE_NAME = "request_queue";
    private static final String RESPONSE_QUEUE_NAME = "response_queue";

    public static void main(String[] args) throws Exception {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");
        factory.setUsername("guest");
        factory.setPassword("guest");
        
        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {
            
            channel.queueDeclare(QUEUE_NAME, false, false, false, null);
            channel.queueDeclare(RESPONSE_QUEUE_NAME, false, false, false, null);
            
            String message = "Hello RabbitMQ!";
            channel.basicPublish("", QUEUE_NAME, null, message.getBytes("UTF-8"));
            System.out.println(" [x] Sent: " + message);
            
            GetResponse response = channel.basicGet(RESPONSE_QUEUE_NAME, true);
            if (response != null) {
                String responseMessage = new String(response.getBody(), "UTF-8");
                System.out.println(" [.] Received response: " + responseMessage);
            }
        }
    }
}
```

### Receiver Application

The receiver application will listen to the request queue, process the request, and send back the response message. Here is an example code snippet:

```java
import com.rabbitmq.client.*;

public class Receiver {

    private static final String QUEUE_NAME = "request_queue";
    private static final String RESPONSE_QUEUE_NAME = "response_queue";

    public static void main(String[] args) throws Exception {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");
        factory.setUsername("guest");
        factory.setPassword("guest");
        
        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {
            
            channel.queueDeclare(QUEUE_NAME, false, false, false, null);
            channel.queueDeclare(RESPONSE_QUEUE_NAME, false, false, false, null);
            channel.basicQos(1);
            
            System.out.println(" [*] Waiting for requests. Press CTRL+C to exit.");
            
            DeliverCallback deliverCallback = (consumerTag, delivery) -> {
                String requestMessage = new String(delivery.getBody(), "UTF-8");
                System.out.println(" [x] Received request: " + requestMessage);
                
                // Process the request and generate the response
                String responseMessage = "Response to: " + requestMessage;
                
                channel.basicPublish("", RESPONSE_QUEUE_NAME, null, responseMessage.getBytes("UTF-8"));
                System.out.println(" [.] Sent response: " + responseMessage);
                channel.basicAck(delivery.getEnvelope().getDeliveryTag(), false);
            };
            
            channel.basicConsume(QUEUE_NAME, false, deliverCallback, consumerTag -> {});
            
            while (true) {
                // Keep the receiver running
            }
        }
    }
}
```

## Conclusion

In this blog post, we learned how to implement the request-response pattern in Java using RabbitMQ. The sender application sends a request message, and the receiver application processes the request and sends back a response. RabbitMQ handles the message routing and ensures reliable delivery.

By leveraging RabbitMQ's request-response pattern, you can build scalable and robust distributed systems that communicate efficiently. Start experimenting with RabbitMQ today and explore the vast possibilities it offers for building messaging applications.

#rabbitmq #java