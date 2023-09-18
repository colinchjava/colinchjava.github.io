---
layout: post
title: "RabbitMQ integration with Apache NiFi in Java"
description: " "
date: 2023-09-18
tags: [hashtags]
comments: true
share: true
---

In today's data-driven world, it's essential to have a robust and efficient way to handle data processing and messaging. RabbitMQ, a popular messaging queue, and Apache NiFi, a powerful data integration platform, are two tools that can be combined to create a seamless data processing pipeline. In this blog post, we will explore how to integrate RabbitMQ with Apache NiFi using Java.

## Prerequisites
Before we begin, make sure you have the following:
- RabbitMQ server installed and running
- Apache NiFi installed and running

## Step 1: Setting Up RabbitMQ
First, let's set up the RabbitMQ messaging queue. Follow these steps:
1. Open the RabbitMQ management console by visiting `http://localhost:15672` in your web browser.
2. Login using the default credentials (username: `guest`, password: `guest`).
3. Create a new queue to store the incoming messages.

## Step 2: Configuring Apache NiFi
Now, let's configure Apache NiFi to consume messages from the RabbitMQ queue. Follow these steps:
1. Open the Apache NiFi user interface by visiting `http://localhost:8080/nifi` in your web browser.
2. Drag and drop a "RabbitMQ Consumer" processor onto the canvas.
3. In the properties panel of the processor, configure the following settings:
   - **RabbitMQ Hosts**: Specify the hostname(s) of your RabbitMQ server.
   - **Queue Name**: Set the name of the RabbitMQ queue you created in step 1.
   - **Username** and **Password**: Set the RabbitMQ credentials if required.
4. Connect the RabbitMQ Consumer processor to the desired downstream processors for further data processing.

## Step 3: Writing the Java Code
To interact with RabbitMQ from Apache NiFi, we need to write custom Java code. Here's an example:

```java
import org.apache.nifi.annotation.behavior.InputRequirement;
import org.apache.nifi.annotation.behavior.ReadsAttributes;
import org.apache.nifi.annotation.behavior.Stateful;
import org.apache.nifi.annotation.documentation.CapabilityDescription;
import org.apache.nifi.annotation.documentation.Tags;
import org.apache.nifi.annotation.lifecycle.OnScheduled;
import org.apache.nifi.components.PropertyDescriptor;
import org.apache.nifi.processor.AbstractProcessor;
import org.apache.nifi.processor.ProcessContext;
import org.apache.nifi.processor.ProcessSession;
import org.apache.nifi.processor.ProcessorInitializationContext;
import org.apache.nifi.processor.Relationship;
import org.apache.nifi.processor.exception.ProcessException;
import org.apache.nifi.processor.util.StandardValidators;

import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;

@Tags({"RabbitMQ", "Integration", "Messaging"})
@InputRequirement(InputRequirement.Requirement.INPUT_REQUIRED)
@CapabilityDescription("Custom processor to consume messages from RabbitMQ queue.")
@ReadsAttributes({})
@Stateful(scopes = Scope.LOCAL, description = "Stores the RabbitMQ connection")
public class RabbitMQConsumerProcessor extends AbstractProcessor {

    private static final PropertyDescriptor RABBITMQ_HOST = new PropertyDescriptor
            .Builder().name("RabbitMQ Hosts")
            .description("Comma-separated list of RabbitMQ hosts.")
            .required(true)
            .addValidator(StandardValidators.NON_EMPTY_VALIDATOR)
            .build();

    private static final PropertyDescriptor QUEUE_NAME = new PropertyDescriptor
            .Builder().name("Queue Name")
            .description("Name of the RabbitMQ queue.")
            .required(true)
            .addValidator(StandardValidators.NON_EMPTY_VALIDATOR)
            .build();

    private static final Relationship SUCCESS = new Relationship.Builder()
            .name("success")
            .description("Success relationship")
            .build();

    private ConnectionFactory connectionFactory;
    private Connection connection;
    private Channel channel;

    @Override
    protected void init(ProcessorInitializationContext context) {
        connectionFactory = new ConnectionFactory();
    }

    @Override
    public final List<PropertyDescriptor> getSupportedPropertyDescriptors() {
        return ImmutableList.of(RABBITMQ_HOST, QUEUE_NAME);
    }

    @Override
    public final Set<Relationship> getRelationships() {
        return ImmutableSet.of(SUCCESS);
    }

    @OnScheduled
    public void onScheduled(ProcessContext context) {
        try {
            connectionFactory.setHost(context.getProperty(RABBITMQ_HOST).getValue());
            connection = connectionFactory.newConnection();
            channel = connection.createChannel();
            channel.queueDeclare(context.getProperty(QUEUE_NAME).getValue(), false, false, false, null);
        } catch (Exception e) {
            getLogger().error("Failed to establish RabbitMQ connection", e);
            throw new ProcessException("Failed to establish RabbitMQ connection", e);
        }
    }

    @Override
    public void onTrigger(ProcessContext context, ProcessSession session) {
        try {
            // Consume messages from RabbitMQ queue and process them

            // Transfer flowfile to downstream processors

            session.transfer(session.get(), SUCCESS);
            session.commit();
        } catch (Exception e) {
            getLogger().error("Failed to consume messages from RabbitMQ queue", e);
            session.rollback();
        }
    }

    @OnShutdown
    public void onShutdown() {
        try {
            channel.close();
            connection.close();
        } catch (Exception e) {
            getLogger().warn("Failed to close RabbitMQ connection", e);
        }
    }
}
```

## Conclusion
By integrating RabbitMQ with Apache NiFi using Java, you can create a powerful data processing pipeline that can handle large volumes of data with ease. With the ability to consume messages from RabbitMQ and perform custom processing in Apache NiFi, you have the flexibility to create a wide range of data-driven applications.

#hashtags: RabbitMQIntegration, ApacheNiFiInJava