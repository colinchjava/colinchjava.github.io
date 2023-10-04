---
layout: post
title: "Reactive programming with messaging systems in Java"
description: " "
date: 2023-09-29
tags: [ReactiveProgramming]
comments: true
share: true
---

Reactive programming has become an increasingly popular paradigm for building scalable and resilient applications. It allows developers to handle asynchronous events and streams of data in a more efficient and declarative manner. When combined with messaging systems, reactive programming can provide even greater flexibility and scalability.

In this blog post, we will explore how to leverage reactive programming with messaging systems in Java, focusing on two popular messaging systems: Apache Kafka and RabbitMQ.

## Apache Kafka

Apache Kafka is a distributed streaming platform that allows for the building of real-time data pipelines and streaming applications. It provides a fault-tolerant and scalable approach to handle large amounts of data.

To use Kafka with Java in a reactive way, we can leverage the Reactive Kafka library, which provides a reactive API for interacting with Kafka. With Reactive Kafka, we can easily subscribe to Kafka topics and consume messages as an infinite stream.

Here's an example of how to consume messages from a Kafka topic using Reactive Kafka:

```java
import akka.kafka.ConsumerMessage.CommittableMessage;
import akka.kafka.scaladsl.Consumer;
import akka.stream.Materializer;
import akka.stream.javadsl.Sink;
import akka.stream.javadsl.Source;
import org.apache.kafka.clients.consumer.ConsumerConfig;
import org.apache.kafka.common.serialization.StringDeserializer;
import akka.actor.ActorSystem;
import akka.kafka.scaladsl.Consumer;
import akka.kafka.scaladsl.Producer;
import akka.kafka.ProducerSettings;
import akka.kafka.ConsumerSettings;
import akka.stream.Materializer;
import akka.stream.javadsl.Source;
import akka.stream.javadsl.Sink;
import com.typesafe.config.ConfigFactory;
import java.util.Collections;
import java.util.concurrent.CompletionStage;
import org.apache.kafka.clients.producer.ProducerRecord;
import org.apache.kafka.common.serialization.StringDeserializer;
import org.apache.kafka.common.serialization.StringSerializer;

public class KafkaConsumer {
  public static void main(String[] args) {
    ActorSystem system = ActorSystem.create("example");
    Materializer materializer = Materializer.createMaterializer(system);

    String topic = "my-topic";
    String groupId = "my-group";
    String bootstrapServers = "localhost:9092";

    // Create consumer settings
    ConsumerSettings<String, String> consumerSettings =
        ConsumerSettings.create(ConfigFactory.load(), new StringDeserializer(), new StringDeserializer())
            .withBootstrapServers(bootstrapServers)
            .withGroupId(groupId)
            .withProperty(ConsumerConfig.AUTO_OFFSET_RESET_CONFIG, "earliest");

    // Create a source that consumes messages from the Kafka topic
    Source<CommittableMessage<String, String>, Consumer.Control> source =
        Consumer.plainSource(consumerSettings, Subscriptions.topics(topic));

    // Process the consumed messages
    source
        .map(CommittableMessage::value)
        .runWith(Sink.foreach(System.out::println), materializer);
  }
}
```

In this example, we create a Kafka consumer using the Reactive Kafka library. We configure the consumer settings, including the bootstrap servers, group ID, and auto offset reset. Then we create a source that consumes messages from a specified Kafka topic. Finally, we process the consumed messages by printing them to the console.

## RabbitMQ

RabbitMQ is a robust and flexible messaging broker that enables communication between different systems. It is widely used for building microservices architectures and decoupling various components of an application.

To use RabbitMQ with Java in a reactive way, we can use the RabbitMQ Java client and combine it with reactive frameworks like Reactor or RxJava.

Here's an example of how to consume messages from a RabbitMQ queue using Reactor:

```java
import reactor.core.publisher.Mono;
import reactor.rabbitmq.*;
import reactor.core.publisher.Flux;
import reactor.rabbitmq.*;
import reactor.core.publisher.Mono;
import java.util.UUID;

public class RabbitMQConsumer {
  public static void main(String[] args) throws InterruptedException {
    ConnectionFactory connectionFactory = new ConnectionFactory();
    connectionFactory.setHost("localhost");

    String queueName = "my-queue";

    // Create a Mono with connection and channel
    Mono<AMQP.Connection> connectionMono =
        Mono.fromConnectionFactory(connectionFactory)
            .doOnNext(connection -> System.out.println("Connected to RabbitMQ"));

    connectionMono.flatMapMany(
        connection ->
            connection
                .createChannel()
                .flatMapMany(
                    channel ->
                        channel
                            .declareQueue(
                                QueueSpecification.queue(queueName).durable(true))
                            .thenReturn(channel)))
        .flatMap(channel -> channel.basicConsume(queueName))
        .subscribe(
            delivery ->
                System.out.println(
                    "Consumed message: " + new String(delivery.getBody())),
            Throwable::printStackTrace,
            () -> System.out.println("Complete"));
  }
}
```

In this example, we create a RabbitMQ consumer using the RabbitMQ Java client and Reactor. We configure the connection factory with the RabbitMQ host. Then we create a Mono with the connection and channel. We declare a durable queue and consume messages from it. Finally, we process the consumed messages by printing them to the console.

# Conclusion

Reactive programming, when combined with messaging systems like Apache Kafka and RabbitMQ, provides a powerful way to handle asynchronous events and streams of data in Java. We explored how to consume messages from Kafka and RabbitMQ in a reactive way using the Reactive Kafka library and Reactor. By leveraging these tools, developers can build more scalable and resilient applications. #ReactiveProgramming #Java