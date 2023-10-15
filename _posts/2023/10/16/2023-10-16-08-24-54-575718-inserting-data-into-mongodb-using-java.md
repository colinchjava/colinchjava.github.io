---
layout: post
title: "Inserting data into MongoDB using Java"
description: " "
date: 2023-10-16
tags: [mongodb]
comments: true
share: true
---

MongoDB is a popular NoSQL database that allows flexible and scalable storage of data. It provides a document-oriented approach to data modeling and is widely used in modern web applications.

Java, as a robust and versatile programming language, is well-suited for interacting with databases like MongoDB. In this tutorial, we will explore how to insert data into MongoDB using Java.

## Prerequisites

Before we get started, make sure you have the following:

- Java Development Kit (JDK) installed
- MongoDB Java driver added to your project (you can use Maven or Gradle for dependency management)

## Connecting to MongoDB

To connect to MongoDB from Java, we first need to establish a connection to the MongoDB server. Here's an example of how to do that:

```java
import com.mongodb.MongoClient;
import com.mongodb.client.MongoDatabase;

public class MongoDBExample {
    public static void main(String[] args) {
        // Create MongoClient
        MongoClient mongoClient = new MongoClient("localhost", 27017);
        
        // Access database
        MongoDatabase database = mongoClient.getDatabase("mydb");
        
        System.out.println("Connected to MongoDB successfully");
        
        // Close the connection
        mongoClient.close();
    }
}
```

In the above code, we create a `MongoClient` object by passing the server address and port number. Then we access the desired database using `getDatabase` method. Finally, we can print a message to confirm the connection and close the connection using `close` method.

## Inserting Data into MongoDB

Once we have established a connection, we can insert data into a collection in MongoDB.

```java
import com.mongodb.MongoClient;
import com.mongodb.client.MongoCollection;
import com.mongodb.client.MongoDatabase;
import org.bson.Document;

public class MongoDBExample {
    public static void main(String[] args) {
        MongoClient mongoClient = new MongoClient("localhost", 27017);
        MongoDatabase database = mongoClient.getDatabase("mydb");

        // Get the collection
        MongoCollection<Document> collection = database.getCollection("myCollection");

        // Prepare the document to be inserted
        Document document = new Document("name", "John Doe")
                                  .append("age", 30)
                                  .append("email", "johndoe@example.com");

        // Insert the document
        collection.insertOne(document);

        System.out.println("Data inserted into MongoDB successfully");

        mongoClient.close();
    }
}
```

In the code above, we first get the collection using `getCollection` method. Then we create a `Document` object and populate it with the data we want to insert. Finally, we use the `insertOne` method to insert the document into the collection.

## Conclusion

In this tutorial, we have learned how to connect to MongoDB from Java and insert data into a collection. MongoDB's flexibility and Java's ease of use make them a powerful combination for handling data storage in modern applications.

For more information and advanced operations with MongoDB and Java, refer to the [official MongoDB Java driver documentation](https://mongodb.github.io/mongo-java-driver/).

#mongodb #java