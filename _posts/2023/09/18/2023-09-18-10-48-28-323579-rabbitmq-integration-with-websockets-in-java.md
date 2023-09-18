---
layout: post
title: "RabbitMQ integration with WebSockets in Java"
description: " "
date: 2023-09-18
tags: []
comments: true
share: true
---

## Introduction
RabbitMQ is a powerful and versatile messaging broker that can be used to implement scalable and reliable communication between different components in a distributed system. The WebSocket protocol, on the other hand, provides a full-duplex communication channel over a single TCP connection, making it ideal for real-time messaging applications.

In this blog post, we will explore how to integrate RabbitMQ with WebSockets in Java to build an efficient and robust messaging system.

## Setting Up RabbitMQ
Before we can start integrating RabbitMQ with WebSockets, we need to have RabbitMQ up and running. You can download RabbitMQ from the official website at [www.rabbitmq.com](https://www.rabbitmq.com) and follow the installation instructions for your specific platform.

Once RabbitMQ is installed, start the RabbitMQ server and ensure that it is running on the default port (5672). You can access the RabbitMQ management console by navigating to [http://localhost:15672](http://localhost:15672) in your web browser. The default username and password are "guest".

## Adding WebSocket Support to your Java Application
To enable WebSocket support in your Java application, you can use a library like Spring Boot or Java EE. In this example, we will use Spring Boot, which provides a convenient way to create WebSocket-based applications.

First, create a new Maven project and add the following dependencies to your `pom.xml` file:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-websocket</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-amqp</artifactId>
    </dependency>
</dependencies>
```

Next, create a new class `WebSocketConfig` and add the following code:

```java
@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {

    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/ws").withSockJS();
    }

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.enableStompBrokerRelay("/topic")
                .setRelayHost("localhost")
                .setRelayPort(61613)
                .setClientLogin("guest")
                .setClientPasscode("guest");
        registry.setApplicationDestinationPrefixes("/app");
    }
}
```

In this configuration class, we define the WebSocket endpoint (/ws) and configure the message broker to relay messages to the "/topic" destination. We also set the RabbitMQ connection details, including the host, port, username, and password.

## Publishing and Subscribing to Messages
To publish and subscribe to messages using RabbitMQ and WebSockets, we first need to define a message model and a controller class.

Create a new class `ChatMessage` with the following code:

```java
public class ChatMessage {
    private String content;
    // getters and setters
}
```

Next, create a new class `ChatController` and add the following code:

```java
@Controller
public class ChatController {

    @MessageMapping("/chat")
    @SendTo("/topic/messages")
    public ChatMessage sendMessage(ChatMessage message) {
        return message;
    }
}
```

In this controller class, we define a method that handles incoming messages ("/chat") and sends them to the "/topic/messages" destination.

## Testing the Integration
To test the integration, start your Java application and open two web browsers. In each browser, navigate to [http://localhost:8080](http://localhost:8080) to establish WebSocket connections.

In one browser, open the browser console and run the following JavaScript code:

```javascript
var socket = new WebSocket("ws://localhost:8080/ws");
socket.onopen = function() {
    console.log("WebSocket connection established!");
    var message = { content: "Hello, RabbitMQ!" };
    socket.send(JSON.stringify(message));
};
```

In the other browser, open the browser console and run the following JavaScript code:

```javascript
var socket = new WebSocket("ws://localhost:8080/ws");
socket.onmessage = function(event) {
    var message = JSON.parse(event.data);
    console.log("Received message: " + message.content);
};
```

You should see the message "Hello, RabbitMQ!" being printed in the console of the second browser, indicating that RabbitMQ successfully relayed the message between the two WebSocket connections.

## Conclusion
In this blog post, we explored how to integrate RabbitMQ with WebSockets in Java. We learned how to set up RabbitMQ, add WebSocket support to a Java application using Spring Boot, and publish and subscribe to messages using RabbitMQ and WebSockets.

Integrating RabbitMQ with WebSockets can greatly enhance the real-time capabilities of your Java applications, enabling efficient and reliable communication between different components.