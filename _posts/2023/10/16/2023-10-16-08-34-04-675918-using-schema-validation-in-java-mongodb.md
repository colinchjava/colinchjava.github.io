---
layout: post
title: "Using schema validation in Java MongoDB"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

MongoDB is a popular NoSQL database that provides high performance and scalability. One of the powerful features of MongoDB is schema validation, which allows you to define rules for the structure and data types of your documents.

Schema validation can help maintain data integrity and ensure that documents inserted into a collection adhere to specific criteria. In this article, we will explore how to use schema validation in Java MongoDB applications.

## Prerequisites

Before we dive into the code examples, make sure you have the following prerequisites set up:

- Java Development Kit (JDK) installed on your machine
- MongoDB Java driver added to your project as a dependency

You can add the MongoDB Java driver to your project using Maven or Gradle. Here is an example Maven dependency:

```xml
<dependency>
    <groupId>org.mongodb</groupId>
    <artifactId>mongo-java-driver</artifactId>
    <version>3.12.7</version>
</dependency>
```

## Enabling Schema Validation

To enable schema validation, you need to define a JSON schema and associate it with a collection in MongoDB. The JSON schema specifies the rules for validating the structure and data types of documents.

Here is an example JSON schema that ensures the "name" field is a string and the "age" field is an integer:

```json
{
  "bsonType": "object",
  "required": ["name", "age"],
  "properties": {
    "name": {
      "bsonType": "string"
    },
    "age": {
      "bsonType": "int"
    }
  }
}
```

To associate this schema with a collection in Java, you can use the `MongoCollection.createCollection()` method and pass the `CollectionOptions` object with the schema validation definition. Here is an example:

```java
MongoClient mongoClient = new MongoClient("localhost", 27017);
MongoDatabase database = mongoClient.getDatabase("mydb");

MongoCollection<Document> collection = database.getCollection("mycollection");

Document schemaValidation = new Document("validator", Document.parse(schemaJson));
collection.createCollection("mycollection", new CollectionOptions().validationOptions(schemaValidation));
```

In the above code, `schemaJson` represents the JSON schema string. You can read the schema from a file or directly define it in your code.

## Inserting Documents with Validation

Once schema validation is enabled for a collection, MongoDB will automatically validate each document before inserting it into the collection. If a document fails to meet the validation rules, MongoDB will throw an exception, and the insert operation will fail.

Here is an example of inserting a document into a validated collection:

```java
Document document = new Document("name", "John Doe")
        .append("age", 30);

collection.insertOne(document);
```

In this example, the inserted document has a valid structure and data types according to the schema. If any required fields are missing or the data types don't match, the insert operation will be rejected.

## Updating Documents with Validation

Schema validation also applies when updating documents in a validated collection. If an update operation would result in a document that violates the validation rules, MongoDB will reject the update and throw an exception.

Here is an example of updating a document in a validated collection:

```java
Bson filter = Filters.eq("name", "John Doe");
Bson update = Updates.set("age", 35);

collection.updateOne(filter, update);
```

In this example, the update operation sets the "age" field to 35 for the document with the name "John Doe". If the update would violate the validation rules, for example by setting the "age" field to a string instead of an integer, the operation will fail.

## Conclusion

Schema validation in MongoDB provides a powerful tool for maintaining data integrity and structure. By defining rules for the structure and data types of documents, you can ensure the consistency of your data.

In this article, we explored how to use schema validation in Java MongoDB applications. We learned how to enable schema validation, insert documents, and update documents while adhering to the validation rules.

By leveraging schema validation, you can take full advantage of MongoDB's flexible yet structured data storage capabilities. It allows you to enforce data quality and maintain a well-defined data model in your applications.

**References:**
- [Official MongoDB Java Driver Documentation](https://mongodb.github.io/mongo-java-driver/4.2/)
- [MongoDB Schema Validation](https://docs.mongodb.com/manual/core/schema-validation/)