---
layout: post
title: "RabbitMQ integration with Apache Camel-Kafka-Quarkus connector in Java"
description: " "
date: 2023-09-18
tags: [RabbitMQIntegration, ApacheCamelKafkaQuarkus]
comments: true
share: true
---

RabbitMQ is a popular message broker that provides reliable message delivery between different applications or services. Apache Camel-Kafka-Quarkus connector is a lightweight integration framework that allows seamless integration of RabbitMQ with Apache Kafka and Quarkus applications.

In this blog post, we will explore how to integrate RabbitMQ with Apache Camel-Kafka-Quarkus connector in Java, demonstrating a simple example of sending and consuming messages.

## Prerequisites
Before we begin, make sure you have the following prerequisites installed:
- JDK 8 or higher
- Apache Kafka
- RabbitMQ server

## Set up the Project
We will start by setting up a new Quarkus project using Maven. Open a terminal and execute the following command:

```bash
mvn io.quarkus:quarkus-maven-plugin:1.13.7.Final:create -DprojectGroupId=com.example -DprojectArtifactId=rabbitmq-integration -DprojectVersion=1.0-SNAPSHOT -DclassName="com.example.RabbitMQIntegrationResource" -Dextensions="kafka,quartz,rabbitmq"
```

This command will create a new Quarkus project with the necessary dependencies for Kafka, Quartz, and RabbitMQ.

## Configure RabbitMQ Connection
In the `application.properties` file, configure the RabbitMQ connection properties:

```properties
quarkus.rabbitmq.username=admin
quarkus.rabbitmq.password=admin123
quarkus.rabbitmq.host=localhost
quarkus.rabbitmq.port=5672
quarkus.rabbitmq.virtual-host=/
```

Make sure to adjust the values according to your RabbitMQ server configuration.

## Implement Message Producer
Next, we'll implement the message producer class, responsible for sending messages to RabbitMQ. Create a new class `RabbitMQProducer`:

```java
import javax.enterprise.context.ApplicationScoped;

import org.apache.camel.ProducerTemplate;

@ApplicationScoped
public class RabbitMQProducer {

    @Inject
    private ProducerTemplate producerTemplate;

    public void sendMessage(String message) {
        producerTemplate.sendBody("rabbitmq:my-exchange?routingKey=my-queue", message);
    }
}
```

The `sendMessage` method sends a message to RabbitMQ exchange named "my-exchange" with a routing key "my-queue". Adjust these values based on your RabbitMQ setup.

## Implement Message Consumer
Now let's implement the message consumer class that will consume messages from RabbitMQ. Create a new class `RabbitMQConsumer`:

```java
import javax.enterprise.context.ApplicationScoped;

import org.apache.camel.builder.RouteBuilder;

@ApplicationScoped
public class RabbitMQConsumer extends RouteBuilder {

    @Override
    public void configure() throws Exception {
        from("rabbitmq:my-exchange?queue=my-queue")
            .to("log:received")
            .bean(this, "processMessage");
    }

    public void processMessage(String message) {
        // process the received message
    }
}
```

The `configure` method sets up a route to consume messages from the RabbitMQ exchange named "my-exchange" with a queue named "my-queue". Adjust these values according to your RabbitMQ configuration. The received messages will be logged and passed to the `processMessage` method for further processing.

## Use the Producer and Consumer
Finally, let's use our producer and consumer classes to send and consume messages. Modify the `RabbitMQIntegrationResource` class as follows:

```java
import javax.inject.Inject;
import javax.ws.rs.GET;
import javax.ws.rs.Path;

@Path("/rabbitmq")
public class RabbitMQIntegrationResource {

    @Inject
    private RabbitMQProducer producer;

    @GET
    @Path("/send")
    public void sendMessage() {
        producer.sendMessage("Hello, RabbitMQ!");
    }
}
```

Now, when you access the `/rabbitmq/send` endpoint, a message will be sent to RabbitMQ.

To consume the messages, you can run the Quarkus application and monitor the logs for the "received" message.

## Conclusion
In this blog post, we explored how to integrate RabbitMQ with the Apache Camel-Kafka-Quarkus connector in Java. We set up a Quarkus project, configured the RabbitMQ connection, implemented a message producer, and consumed messages using a message consumer. With this integration, you can easily exchange messages between your applications or services using RabbitMQ as the message broker.

Give it a try and unleash the power of RabbitMQ integration in your Java applications!

## #RabbitMQIntegration #ApacheCamelKafkaQuarkus