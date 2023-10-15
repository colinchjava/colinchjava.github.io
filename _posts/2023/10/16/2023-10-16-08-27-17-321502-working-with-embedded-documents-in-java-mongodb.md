---
layout: post
title: "Working with embedded documents in Java MongoDB"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

MongoDB is a popular NoSQL database that allows for the storage of dynamic schemas. One of the key features of MongoDB is the ability to work with embedded documents, which are documents nested within other documents. This provides a flexible data model and allows for the storage of complex data structures.

In this tutorial, we will explore how to work with embedded documents in Java using the MongoDB Java driver.

## Table of Contents
- [Prerequisites](#prerequisites)
- [Connecting to the MongoDB Server](#connecting-to-the-mongodb-server)
- [Creating and Inserting Documents](#creating-and-inserting-documents)
- [Accessing Embedded Documents](#accessing-embedded-documents)
- [Updating Embedded Documents](#updating-embedded-documents)
- [Deleting Embedded Documents](#deleting-embedded-documents)
- [Conclusion](#conclusion)
- [References](#references)

## Prerequisites
To follow along with this tutorial, make sure you have the following:

- Java Development Kit (JDK) installed on your machine
- MongoDB server installed and running
- MongoDB Java driver added to your project

## Connecting to the MongoDB Server
Before we can start working with embedded documents, we need to establish a connection to the MongoDB server using the Java driver. Here's an example of how to connect to a local MongoDB server:

```java
import com.mongodb.MongoClient;
import com.mongodb.client.MongoDatabase;

public class MongoDBConnection {
    public static void main(String[] args) {
        // Connect to the MongoDB server
        MongoClient mongoClient = new MongoClient("localhost", 27017);

        // Access the test database
        MongoDatabase database = mongoClient.getDatabase("test");

        // Do something with the database

        // Close the connection
        mongoClient.close();
    }
}
```

Make sure to replace `"localhost"` with the appropriate hostname if your MongoDB server is running on a different machine.

## Creating and Inserting Documents
To create and insert documents with embedded documents, we can use the `Document` class provided by the MongoDB Java driver. Here's an example of how to create a document with an embedded document and insert it into a collection:

```java
import org.bson.Document;

public class InsertDocument {
    public static void main(String[] args) {
        // Create the main document
        Document mainDocument = new Document("name", "John Doe");

        // Create the embedded document
        Document address = new Document("street", "123 Main St")
                .append("city", "New York")
                .append("state", "NY");

        // Add the embedded document to the main document
        mainDocument.append("address", address);

        // Insert the document into the collection
        collection.insertOne(mainDocument);
    }
}
```

## Accessing Embedded Documents
To access embedded documents, we can use dot notation to specify the path to the embedded document. Here's an example of how to access an embedded document:

```java
import org.bson.Document;

public class AccessEmbeddedDocument {
    public static void main(String[] args) {
        // Retrieve the main document by some criteria
        Document mainDocument = collection.find(eq("name", "John Doe")).first();

        // Access the embedded document
        Document address = (Document) mainDocument.get("address");

        // Access fields within the embedded document
        String city = address.getString("city");
        String state = address.getString("state");

        // Do something with the fields
    }
}
```

## Updating Embedded Documents
To update an embedded document, you can use the `$set` operator to modify specific fields within the embedded document. Here's an example of how to update an embedded document:

```java
import org.bson.Document;

public class UpdateEmbeddedDocument {
    public static void main(String[] args) {
        // Retrieve the main document by some criteria
        Document mainDocument = collection.find(eq("name", "John Doe")).first();

        // Update the embedded document
        mainDocument.get("address", Document.class).put("city", "San Francisco");

        // Update the document in the collection
        collection.replaceOne(eq("_id", mainDocument.getObjectId("_id")), mainDocument);
    }
}
```

## Deleting Embedded Documents
To delete an embedded document, you can use the `$unset` operator to remove specific fields within the embedded document. Here's an example of how to delete an embedded document:

```java
import org.bson.Document;

public class DeleteEmbeddedDocument {
    public static void main(String[] args) {
        // Retrieve the main document by some criteria
        Document mainDocument = collection.find(eq("name", "John Doe")).first();

        // Delete the embedded document field
        mainDocument.remove("address");

        // Update the document in the collection
        collection.replaceOne(eq("_id", mainDocument.getObjectId("_id")), mainDocument);
    }
}
```

## Conclusion
Working with embedded documents in Java MongoDB allows for the creation and manipulation of complex data structures. By utilizing the MongoDB Java driver and the `Document` class, you can easily work with embedded documents in your Java applications.

I hope you found this tutorial helpful! If you have any questions or feedback, please feel free to reach out.

## References
- [MongoDB Java Driver Documentation](https://docs.mongodb.com/drivers/java/)
- [MongoDB Manual: Embedded Documents](https://docs.mongodb.com/manual/tutorial/model-embedded-one-to-one-relationships-between-documents/)