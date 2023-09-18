---
layout: post
title: "RabbitMQ integration with Jetty in Java"
description: " "
date: 2023-09-18
tags: [RabbitMQ, Jetty]
comments: true
share: true
---

## Setting up RabbitMQ

Before we dive into the integration, make sure you have RabbitMQ installed and running on your machine. You can download RabbitMQ from the official website and follow the installation instructions for your operating system.

Once RabbitMQ is up and running, you will need to create a queue and exchange. The queue represents a message destination, while the exchange determines how messages are distributed to queues.

To create a queue and exchange, you can use the RabbitMQ management console or write a simple Java program using the RabbitMQ Java client library.

```java
import com.rabbitmq.client.ConnectionFactory;
import com.rabbitmq.client.Connection;
import com.rabbitmq.client.Channel;

public class RabbitMQSetup {
    private final static String QUEUE_NAME = "my_queue";
    private final static String EXCHANGE_NAME = "my_exchange";

    public static void main(String[] argv) throws Exception {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");

        try (Connection connection = factory.newConnection();
             Channel channel = connection.createChannel()) {
            channel.queueDeclare(QUEUE_NAME, false, false, false, null);
            channel.exchangeDeclare(EXCHANGE_NAME, "direct");
            channel.queueBind(QUEUE_NAME, EXCHANGE_NAME, "");
        }
    }
}
```

The above code sets up a connection to RabbitMQ running on the local machine and declares a queue and an exchange. The `channel.queueBind` method binds the queue to the exchange.

## Integrating RabbitMQ with Jetty

To integrate RabbitMQ with Jetty, we will use the RabbitMQ Java client library and the Jetty WebSocket API.

First, make sure you have the necessary dependencies in your project. You can use Maven or Gradle to manage your dependencies. Add the following dependencies to your project's build file:

```xml
<dependencies>
    <dependency>
        <groupId>com.rabbitmq</groupId>
        <artifactId>amqp-client</artifactId>
        <version>5.12.0</version>
    </dependency>
    <dependency>
        <groupId>org.eclipse.jetty.websocket</groupId>
        <artifactId>javax-websocket-server-impl</artifactId>
        <version>9.4.44.v20210927</version>
    </dependency>
</dependencies>
```

Next, let's create a WebSocket endpoint in Jetty that will receive messages from RabbitMQ and send them to connected clients.

```java
import com.rabbitmq.client.*;
import org.eclipse.jetty.websocket.api.Session;
import org.eclipse.jetty.websocket.api.annotations.WebSocket;
import org.eclipse.jetty.websocket.api.annotations.OnWebSocketClose;
import org.eclipse.jetty.websocket.api.annotations.OnWebSocketConnect;
import org.eclipse.jetty.websocket.api.annotations.OnWebSocketMessage;
import org.eclipse.jetty.websocket.api.annotations.WebSocketConnectionDropped;

import java.io.IOException;
import java.util.concurrent.TimeoutException;

@WebSocket
public class RabbitMQWebSocketEndpoint {
    private final static String QUEUE_NAME = "my_queue";

    @OnWebSocketConnect
    public void onConnect(Session session) throws IOException, TimeoutException {
        ConnectionFactory factory = new ConnectionFactory();
        factory.setHost("localhost");

        Connection connection = factory.newConnection();
        Channel channel = connection.createChannel();
        channel.basicConsume(QUEUE_NAME, true, (consumerTag, delivery) -> {
            String message = new String(delivery.getBody(), "UTF-8");
            session.getRemote().sendString(message);
        }, consumerTag -> {});

        session.getRemote().sendString("Connected to RabbitMQ");
    }

    @OnWebSocketMessage
    public void onMessage(Session session, String message) {
        // Handle messages received from clients
    }

    @OnWebSocketClose
    public void onClose(Session session, int statusCode, String reason) {
        // Handle WebSocket connection closing
    }

    @WebSocketConnectionDropped
    public void onConnectionDropped(Session session, Throwable throwable) {
        // Handle WebSocket connection dropped
    }
}
```

The above code sets up a WebSocket endpoint using Jetty's annotation-based approach. In the `onConnect` method, we connect to RabbitMQ, consume messages from the queue, and send them to the connected client sessions using the WebSocket's `RemoteEndpoint`. We also send a "Connected to RabbitMQ" message to the client when the connection is established.

Finally, we need to configure Jetty to use our WebSocket endpoint. You can do this by creating a Jetty server and adding the WebSocket endpoint to it.

```java
import org.eclipse.jetty.server.Server;
import org.eclipse.jetty.servlet.ServletContextHandler;
import org.eclipse.jetty.servlet.ServletHolder;

public class JettyServer {
    public static void main(String[] args) throws Exception {
        Server server = new Server(8080);

        ServletContextHandler context = new ServletContextHandler(ServletContextHandler.SESSIONS);
        context.setContextPath("/");
        server.setHandler(context);

        ServletHolder holder = context.addServlet(org.eclipse.jetty.websocket.server.WebSocketServerServlet.class, "/ws/*");
        holder.setInitParameter("javax.websocket.server.ServerEndpoint", "com.example.RabbitMQWebSocketEndpoint");

        server.start();
        server.join();
    }
}
```

The code above creates a Jetty server listening on port 8080. We then create a `ServletContextHandler` and configure the context path. We add a `ServletHolder` for the WebSocket servlet and specify the `ServerEndpoint` class that represents our WebSocket endpoint.

That's it! You've successfully integrated RabbitMQ with Jetty in Java. Messages received by RabbitMQ will now be sent to connected WebSocket clients through the Jetty server.

Remember to start RabbitMQ and run the Jetty server before testing your integration. You can connect WebSocket clients to `ws://localhost:8080/ws/` to receive messages from RabbitMQ.

#RabbitMQ #Jetty