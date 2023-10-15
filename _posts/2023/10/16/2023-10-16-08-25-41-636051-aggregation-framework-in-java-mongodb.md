---
layout: post
title: "Aggregation framework in Java MongoDB"
description: " "
date: 2023-10-16
tags: []
comments: true
share: true
---

MongoDB is a popular NoSQL database that follows a document-oriented data model. It provides a powerful feature called the Aggregation Framework which allows you to perform complex data operations on MongoDB collections.

The Aggregation Framework in MongoDB is analogous to the GROUP BY clause in SQL databases. It provides a way to manipulate and transform documents in a collection, allowing you to perform operations like grouping, filtering, sorting, and calculating aggregate values.

In this blog post, we will explore how to use the Aggregation Framework in Java to perform advanced data operations on MongoDB collections.

## Setting up the MongoDB Java Driver

Before we dive into the Aggregation Framework, let's first set up the MongoDB Java Driver in our project. You can add the following Maven dependency to your project's `pom.xml` file:

```xml
<dependency>
    <groupId>org.mongodb</groupId>
    <artifactId>mongodb-driver-sync</artifactId>
    <version>4.3.3</version>
</dependency>
```

## Aggregation Pipeline

The Aggregation Framework in MongoDB operates on a concept called the "aggregation pipeline". The pipeline is a sequence of stages, where each stage performs a specific data operation. These stages are applied in the order they appear in the pipeline.

An aggregation pipeline typically consists of the following stages:

1. **Matching**: Filters documents based on specific conditions.
2. **Grouping**: Groups matching documents based on specified fields.
3. **Projecting**: Selects specific fields to include or exclude in the output.
4. **Sorting**: Sorts the documents based on specified fields.
5. **Limiting**: Limits the number of documents in the output.
6. **Skipping**: Skips a specified number of documents in the output.
7. **Unwinding**: Deconstructs an array field into multiple documents.
8. **Aggregating**: Performs various aggregation operations like sum, average, etc.

Each stage in the pipeline is represented by a class in the Java MongoDB driver, and you can chain these stages together to build your aggregation pipeline.

## Example Aggregation Query

Let's consider an example where we have a collection of books with the following structure:

```json
{
  "_id": ObjectId("1234567890"),
  "title": "Java Programming",
  "author": "John Doe",
  "price": 39.99,
  "category": "Programming"
}
```

Now, let's say we want to find the average price of books in each category. We can achieve this using the Aggregation Framework in Java as follows:

```java
import com.mongodb.client.AggregateIterable;
import static com.mongodb.client.model.Aggregates.*;
import static com.mongodb.client.model.Filters.*;
import static com.mongodb.client.model.Accumulators.avg;

// Creating the aggregation pipeline
AggregateIterable<Document> pipeline = collection.aggregate(
    List.of(
        match(eq("category", "Programming")), // Filter documents with category: "Programming"
        group("$category", avg("averagePrice", "$price")) // Group by category and calculate average price
    )
);

// Iterating over the results
for (Document document : pipeline) {
    String category = document.getString("_id");
    double averagePrice = document.getDouble("averagePrice");
    System.out.println("Category: " + category + ", Average Price: " + averagePrice);
}
```

In this example, we use the `match` stage to filter documents with the category "Programming", and then the `group` stage to group the matching documents by category and calculate the average price.

Finally, we iterate over the results of the aggregation pipeline and print the category and average price for each category.

## Conclusion

The Aggregation Framework in MongoDB provides a powerful way to perform complex data operations on collections. In this blog post, we explored how to use the Aggregation Framework in Java with the MongoDB Java Driver.

By mastering the Aggregation Framework, you can unlock the full potential of MongoDB and perform advanced analytics and data manipulations with ease.

Give it a try and see how the Aggregation Framework can help you in your MongoDB projects!

**References:**
- [MongoDB Aggregation](https://docs.mongodb.com/manual/aggregation/)
- [MongoDB Java Driver Documentation](https://mongodb.github.io/mongo-java-driver/)