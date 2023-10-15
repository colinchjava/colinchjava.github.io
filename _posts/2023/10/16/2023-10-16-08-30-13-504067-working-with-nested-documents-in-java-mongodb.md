---
layout: post
title: "Working with nested documents in Java MongoDB"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

MongoDB is a popular NoSQL database that allows the storage of documents in a flexible and schema-less format. One of the advantages of MongoDB is its ability to handle nested documents, which can be useful for representing complex data structures.

In this blog post, we will explore how to work with nested documents in Java using the MongoDB Java driver.

## Connecting to MongoDB

Before we can start working with nested documents, we need to establish a connection to the MongoDB server. Here's how we can do it in Java:

```java
import com.mongodb.MongoClient;
import com.mongodb.client.MongoDatabase;

MongoClient mongoClient = new MongoClient("localhost", 27017);
MongoDatabase database = mongoClient.getDatabase("mydb");
```

## Inserting a document with nested fields

To insert a document with nested fields, we can create a `Document` object and use the `append` method to add the nested fields. Here's an example:

```java
import org.bson.Document;

Document book = new Document()
    .append("title", "The Great Gatsby")
    .append("author", "F. Scott Fitzgerald")
    .append("year", 1925)
    .append("publisher", new Document()
        .append("name", "Scribner")
        .append("location", "New York")
    );

database.getCollection("books").insertOne(book);
```

In this example, we create a `Document` object representing a book with nested fields for the publisher. We then insert this document into the "books" collection.

## Querying nested fields

To query for documents with nested fields, we can use the dot notation to specify the path to the nested field. Here's an example:

```java
import com.mongodb.client.FindIterable;
import com.mongodb.client.MongoCursor;

Document query = new Document("publisher.name", "Scribner");
FindIterable<Document> result = database.getCollection("books").find(query);

MongoCursor<Document> cursor = result.iterator();
while (cursor.hasNext()) {
    Document book = cursor.next();
    // Do something with the book document
}

cursor.close();
```

In this example, we create a `Document` object representing the query for books where the publisher's name is "Scribner". We then execute the query using the `find` method and iterate over the result using a cursor.

## Updating nested fields

To update nested fields in a document, we can use the dot notation to specify the path to the nested field. Here's an example:

```java
import com.mongodb.client.result.UpdateResult;

Document query = new Document("publisher.name", "Scribner");
Document update = new Document("$set", new Document("publisher.location", "London"));

UpdateResult result = database.getCollection("books").updateOne(query, update);
System.out.println(result.getModifiedCount() + " document(s) updated.");
```

In this example, we create a `Document` object representing the query for books where the publisher's name is "Scribner". We then use the `$set` operator to update the location field of the publisher to "London". The `updateOne` method is used to perform the update operation.

## Conclusion

Working with nested documents in Java MongoDB allows us to represent complex data structures and perform operations on the nested fields. In this blog post, we covered how to connect to MongoDB, insert documents with nested fields, query for nested fields, and update nested fields.

By leveraging the features of MongoDB and the MongoDB Java driver, we can build powerful and flexible applications that can handle complex data models efficiently.

# References
- [MongoDB Java driver documentation](https://mongodb.github.io/mongo-java-driver/)
- [MongoDB manual on working with nested documents](https://docs.mongodb.com/manual/tutorial/query-for-nested-fields/)