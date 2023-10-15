---
layout: post
title: "Working with audit logs in Java MongoDB"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

In any application, it is crucial to have visibility into the actions performed by users and track changes made to critical data. One way to achieve this is by implementing audit logs. Audit logs record details of user actions, such as who performed the action, what action was taken, and when it occurred. In this article, we will explore how to work with audit logs in Java using MongoDB.

## Table of Contents
- [Setting up MongoDB in Java](#setting-up-mongodb-in-java)
- [Creating an Audit Log Collection in MongoDB](#creating-an-audit-log-collection-in-mongodb)
- [Recording Audit Logs](#recording-audit-logs)
- [Retrieving Audit Logs](#retrieving-audit-logs)
- [Conclusion](#conclusion)

## Setting up MongoDB in Java

To interact with MongoDB in Java, we need to add the MongoDB Java driver to our project's dependencies. We can do this by adding the following Maven dependency to our `pom.xml` file:

```xml
<dependency>
    <groupId>org.mongodb</groupId>
    <artifactId>mongodb-driver-sync</artifactId>
    <version>4.3.1</version>
</dependency>
```

Alternatively, if you are using Gradle, you can add the following dependency to your `build.gradle` file:

```groovy
implementation 'org.mongodb:mongodb-driver-sync:4.3.1'
```

After adding the dependency, we can now proceed to create an audit log collection in MongoDB.

## Creating an Audit Log Collection in MongoDB

First, we need to establish a connection to the MongoDB server using the `MongoClient` class. We can do this by specifying the connection details, such as the hostname and port number:

```java
import com.mongodb.ConnectionString;
import com.mongodb.MongoClientSettings;
import com.mongodb.client.MongoClients;
import com.mongodb.client.MongoClient;

// ConnectionString example: mongodb://localhost:27017
ConnectionString connectionString = new ConnectionString("<YOUR_MONGODB_CONNECTION_STRING>");
MongoClientSettings settings = MongoClientSettings.builder()
        .applyConnectionString(connectionString)
        .retryWrites(true)
        .build();
        
MongoClient mongoClient = MongoClients.create(settings);
```

Once we have a `MongoClient` instance, we can use it to access a database and create a collection specifically for storing audit logs:

```java
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;

MongoDatabase database = mongoClient.getDatabase("<YOUR_DATABASE_NAME>");
MongoCollection<Document> auditLogCollection = database.getCollection("audit_logs");
```

With the audit log collection set up, we can now proceed to record audit logs whenever a user performs an action.

## Recording Audit Logs

To record an audit log, we create a new document using the `Document` class provided by the MongoDB Java driver. This document will contain details such as the user who performed the action, the action itself, and the timestamp.

Here's an example of recording an audit log for a user creating a new record:

```java
import org.bson.Document;

Document auditLog = new Document();
auditLog.append("user", "John Doe");
auditLog.append("action", "create");
auditLog.append("timestamp", new Date());

auditLogCollection.insertOne(auditLog);
```

In this example, we set the `user` field to "John Doe", the `action` field to "create", and the `timestamp` field to the current date and time. Once the document is created, we can insert it into the audit log collection using the `insertOne` method.

## Retrieving Audit Logs

To retrieve audit logs, we can use various methods provided by the MongoDB Java driver. For example, we can retrieve all audit logs sorted by timestamp in descending order:

```java
import com.mongodb.client.FindIterable;

FindIterable<Document> auditLogs = auditLogCollection.find().sort(new Document("timestamp", -1));

for (Document log : auditLogs) {
    System.out.println(log.toJson());
}
```

In this example, we use the `find` method to retrieve all documents from the audit log collection and sort them by the `timestamp` field in descending order. Then, we iterate over the `auditLogs` iterable and print each log using the `toJson` method.

## Conclusion

Implementing audit logs in our Java MongoDB application allows us to track user actions and maintain an audit trail of critical changes. By creating an audit log collection, recording logs, and retrieving them when needed, we can gain valuable insights into the behavior of our application and ensure accountability.