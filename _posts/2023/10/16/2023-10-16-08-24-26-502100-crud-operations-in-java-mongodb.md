---
layout: post
title: "CRUD operations in Java MongoDB"
description: " "
date: 2023-10-16
tags: [mongoDB]
comments: true
share: true
---

MongoDB, a no-SQL database, provides a flexible and scalable solution for storing and retrieving data. In this blog post, we will explore how to perform CRUD (Create, Read, Update, Delete) operations in MongoDB using Java.

## Prerequisites
Before diving into the CRUD operations, make sure you have the following set up in your environment:
- MongoDB installed and running
- Java SDK installed

## Connect to the MongoDB Database
To establish a connection with the MongoDB database, we need to use the MongoDB Java driver. You can include the driver in your Java project using Maven or by downloading the JAR file directly.

Here's an example of how to connect to a MongoDB database using Java:

```java
import com.mongodb.client.MongoClients;
import com.mongodb.client.MongoClient;
	
public class MongoDBConnection {
    public static void main(String[] args) {
        MongoClient mongoClient = MongoClients.create("mongodb://localhost:27017");
        
        // Perform CRUD operations here
        
        mongoClient.close();
    }
}
```

## Create Document (Insert)
To insert a document into MongoDB, we need to create a `Document` object and insert it into the desired collection. Here's an example:

```java
import org.bson.Document;
import com.mongodb.client.MongoCollection;
	
// Assuming you already have a MongoClient object
MongoCollection<Document> collection = mongoClient.getDatabase("mydb").getCollection("mycollection");

Document document = new Document("name", "John Doe")
                        .append("age", 30)
                        .append("email", "john.doe@example.com");

collection.insertOne(document);
```

## Read Documents
To retrieve documents from MongoDB, we can use the `find` method to get a cursor for the matching documents. Here's an example:

```java
import org.bson.Document;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.FindIterable;

// Assuming you already have a MongoClient object and a MongoCollection object
FindIterable<Document> documents = collection.find();

for (Document document : documents) {
    System.out.println(document.toJson());
}
```

## Update Document
To update a document in MongoDB, we use the `updateOne` method and specify the filter criteria and the update operation. Here's an example:

```java
import org.bson.Document;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.UpdateResult;
import static com.mongodb.client.model.Filters.eq;
import static com.mongodb.client.model.Updates.set;

// Assuming you already have a MongoClient object and a MongoCollection object
UpdateResult result = collection.updateOne(eq("name", "John Doe"), set("age", 35));

System.out.println("Modified documents: " + result.getModifiedCount());
```

## Delete Document
To delete a document from MongoDB, we use the `deleteOne` method and specify the filter criteria. Here's an example:

```java
import org.bson.Document;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.DeleteResult;
import static com.mongodb.client.model.Filters.eq;

// Assuming you already have a MongoClient object and a MongoCollection object
DeleteResult result = collection.deleteOne(eq("name", "John Doe"));

System.out.println("Deleted documents: " + result.getDeletedCount());
```

## Conclusion
In this blog post, we've seen how to perform CRUD operations in MongoDB using Java. Remember to handle exceptions and close the MongoDB connection properly. MongoDB's flexibility and scalability make it a great choice for modern application development.

To learn more about MongoDB and its Java driver, refer to the official documentation:
- [MongoDB Java Driver Documentation](https://mongodb.github.io/mongo-java-driver/)
- [MongoDB CRUD Operations](https://docs.mongodb.com/manual/crud/)

#mongoDB #Java