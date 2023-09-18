---
layout: post
title: "RabbitMQ round-robin message distribution in Java"
description: " "
date: 2023-09-18
tags: [RabbitMQ, Java]
comments: true
share: true
---

RabbitMQ is a popular message broker that allows you to implement a message queueing system in your applications. One of the key features of RabbitMQ is its ability to distribute messages among multiple consumers using different distribution mechanisms.

In this blog post, we'll focus on round-robin message distribution, which evenly distributes messages across multiple consumers. This ensures that each consumer gets an equal share of the incoming messages.

## Setting Up RabbitMQ

Before we dive into the round-robin distribution, let's quickly set up RabbitMQ in Java. Make sure you have RabbitMQ installed and running on your machine before proceeding.

To start with, you'll need to include the RabbitMQ client library in your Java project. You can do this by adding the following Maven dependency to your `pom.xml` file:

```xml
<dependency>
    <groupId>com.rabbitmq</groupId>
    <artifactId>amqp-client</artifactId>
    <version>5.13.0</version>
</dependency>
```

Next, create a Java class to establish a connection with the RabbitMQ server:

```java
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;

public class RabbitMQUtils {

    public static Connection createConnection() throws Exception {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");
        return factory.newConnection();
    }
}
```

## Round-Robin Distribution

Now that we have a basic RabbitMQ setup, let's look at how to implement round-robin message distribution. 

First, we'll create multiple consumers that will process the incoming messages:

```java
import com.rabbitmq.client.*;

public class RabbitMQConsumer {

    private static final String QUEUE_NAME = "my_queue";

    public static void main(String[] args) throws Exception {
        Connection connection = RabbitMQUtils.createConnection();
        Channel channel = connection.createChannel();

        channel.queueDeclare(QUEUE_NAME, false, false, false, null);

        channel.basicQos(1); // Set maximum unacknowledged messages to 1

        System.out.println("Waiting for messages...");

        Consumer consumer = new DefaultConsumer(channel) {
            @Override
            public void handleDelivery(String consumerTag, Envelope envelope, AMQP.BasicProperties properties, byte[] body) throws IOException {
                String message = new String(body, "UTF-8");
                System.out.println("Received message: " + message);

                try {
                    // Simulate message processing
                    Thread.sleep(1000);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } finally {
                    channel.basicAck(envelope.getDeliveryTag(), false);
                }
            }
        };

        channel.basicConsume(QUEUE_NAME, false, consumer);
    }
}
```

In the above code, we create a consumer that connects to the RabbitMQ server, declares a queue, and starts listening for messages. The `basicQos` method is used to limit the maximum number of unacknowledged messages to 1, ensuring that the messages are evenly distributed among multiple consumers.

Next, let's implement the producer that publishes messages to the queue:

```java
import com.rabbitmq.client.*;

public class RabbitMQProducer {

    private static final String QUEUE_NAME = "my_queue";

    public static void main(String[] args) throws Exception {
        Connection connection = RabbitMQUtils.createConnection();
        Channel channel = connection.createChannel();

        channel.queueDeclare(QUEUE_NAME, false, false, false, null);

        for (int i = 1; i <= 10; i++) {
            String message = "Message " + i;
            channel.basicPublish("", QUEUE_NAME, null, message.getBytes("UTF-8"));
            System.out.println("Sent message: " + message);
        }

        channel.close();
        connection.close();
    }
}
```

The producer code simply connects to the RabbitMQ server, declares the same queue as the consumer, and publishes 10 messages to the queue.

## Conclusion

By implementing round-robin message distribution in RabbitMQ, you can ensure that multiple consumers receive an equal share of incoming messages. In this blog post, we walked through the process of setting up RabbitMQ in Java and implementing round-robin distribution using consumers and producers.

Remember to add the necessary exception handling and error checking in a real-world scenario. Happy coding!

## #RabbitMQ #Java