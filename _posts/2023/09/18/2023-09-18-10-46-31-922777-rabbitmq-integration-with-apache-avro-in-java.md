---
layout: post
title: "RabbitMQ integration with Apache Avro in Java"
description: " "
date: 2023-09-18
tags: []
comments: true
share: true
---

Apache Avro is a data serialization framework that provides efficient data exchange between systems. RabbitMQ is a popular messaging broker that enables communication between different applications. In this blog post, we will explore how to integrate RabbitMQ with Apache Avro in Java.

## Prerequisites

Before we get started, make sure you have the following prerequisites in place:

1. RabbitMQ server installed and running.
2. Java Development Kit (JDK) installed on your system.
3. Maven or Gradle build tool installed.

## Setting up RabbitMQ

First, let's set up RabbitMQ server and create a new queue and exchange. You can use the RabbitMQ management console or command-line tools to perform these tasks. Once you have created the queue and exchange, note down the queue name and exchange name for later use.

## Setting up Avro

To use Apache Avro in your Java project, you need to add the Avro dependencies to your project's build file (pom.xml for Maven or build.gradle for Gradle). Here is an example of the Maven dependency:

```xml
<dependency>
  <groupId>org.apache.avro</groupId>
  <artifactId>avro</artifactId>
  <version>1.10.2</version>
</dependency>
```

Make sure to update the version number to the latest stable release.

## Creating Avro Schema

The next step is to define your Avro schema. A schema describes the data structure that you will be exchanging between the producer and consumer. Avro schemas are written in JSON format.

Here is an example of a simple Avro schema for a user:

```json
{
  "namespace": "com.example",
  "type": "record",
  "name": "User",
  "fields": [
    {"name": "id", "type": "int"},
    {"name": "name", "type": "string"},
    {"name": "email", "type": "string"}
  ]
}
```

Save this schema in a file (e.g., user.avsc) in your project.

## Generating Java Classes

To work with Avro schemas in Java, you need to generate Java classes from the Avro schema. You can use the Avro Maven plugin or Gradle Avro plugin for this purpose.

Here is an example configuration for the Avro Maven plugin:

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.avro</groupId>
      <artifactId>avro-maven-plugin</artifactId>
      <version>1.10.2</version>
      <executions>
        <execution>
          <phase>generate-sources</phase>
          <goals>
            <goal>schema</goal>
          </goals>
          <configuration>
            <sourceDirectory>${project.basedir}/src/main/avro</sourceDirectory>
            <outputDirectory>${project.build.directory}/generated-sources</outputDirectory>
          </configuration>
        </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

Make sure to update the version number to the latest stable release.

## Producing and Consuming Avro Messages

To produce Avro messages and publish them to RabbitMQ, you need to create a RabbitMQ producer. Here is an example code snippet:

```java
import org.apache.avro.Schema;
import org.apache.avro.generic.GenericData;
import org.apache.avro.generic.GenericRecord;
import org.apache.avro.io.BinaryEncoder;
import org.apache.avro.io.EncoderFactory;
import org.apache.avro.specific.SpecificDatumWriter;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;

public class RabbitMQProducer {

  private static final String QUEUE_NAME = "your_queue_name";
  private static final String EXCHANGE_NAME = "your_exchange_name";

  public static void main(String[] args) {
    try {
      // Create connection and channel
      ConnectionFactory factory = new ConnectionFactory();
      factory.setHost("localhost");
      Connection connection = factory.newConnection();
      Channel channel = connection.createChannel();
      
      // Load Avro schema
      Schema schema = new Schema.Parser().parse(RabbitMQProducer.class.getResourceAsStream("/user.avsc"));
      
      // Create Avro record
      GenericRecord user = new GenericData.Record(schema);
      user.put("id", 1);
      user.put("name", "John Doe");
      user.put("email", "john.doe@example.com");
      
      // Serialize Avro record
      SpecificDatumWriter<GenericRecord> writer = new SpecificDatumWriter<>(schema);
      EncoderFactory encoderFactory = new EncoderFactory();
      BinaryEncoder encoder = encoderFactory.binaryEncoder(System.out, null);
      writer.write(user, encoder);
      encoder.flush();
      
      // Publish Avro message to RabbitMQ
      channel.basicPublish(EXCHANGE_NAME, "", null, encoder);
      
      // Close connection and channel
      channel.close();
      connection.close();
      
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

To consume Avro messages from RabbitMQ, you need to create a RabbitMQ consumer. Here is an example code snippet:

```java
import org.apache.avro.Schema;
import org.apache.avro.generic.GenericData;
import org.apache.avro.generic.GenericRecord;
import org.apache.avro.io.BinaryDecoder;
import org.apache.avro.io.DecoderFactory;
import org.apache.avro.specific.SpecificDatumReader;
import com.rabbitmq.client.Channel;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.DeliverCallback;

public class RabbitMQConsumer {

  private static final String QUEUE_NAME = "your_queue_name";
  private static final String EXCHANGE_NAME = "your_exchange_name";

  public static void main(String[] args) {
    try {
      // Create connection and channel
      ConnectionFactory factory = new ConnectionFactory();
      factory.setHost("localhost");
      Connection connection = factory.newConnection();
      Channel channel = connection.createChannel();
      
      // Declare queue and bind it to the exchange
      channel.queueDeclare(QUEUE_NAME, false, false, false, null);
      channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "");
      
      // Set up callback to handle incoming messages
      DeliverCallback deliverCallback = (consumerTag, delivery) -> {
        BinaryDecoder decoder = DecoderFactory.get().binaryDecoder(delivery.getBody(), null);
        SpecificDatumReader<GenericRecord> reader = new SpecificDatumReader<>(your_generated_avro_class.getClassSchema());
        GenericRecord message = reader.read(null, decoder);
        System.out.println("Received message: " + message);
      };
      
      // Start consuming messages
      channel.basicConsume(QUEUE_NAME, true, deliverCallback, consumerTag -> { });
      
    } catch (Exception e) {
      e.printStackTrace();
    }
  }
}
```

## Conclusion

Integrating RabbitMQ with Apache Avro in Java can enable efficient and reliable data exchange between your applications. By following the steps outlined in this blog post, you can set up RabbitMQ, define Avro schemas, generate Java classes, and produce/consume Avro messages.