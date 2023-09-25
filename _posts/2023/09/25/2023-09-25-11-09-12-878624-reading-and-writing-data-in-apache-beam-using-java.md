---
layout: post
title: "Reading and writing data in Apache Beam using Java"
description: " "
date: 2023-09-25
tags: [ApacheBeam]
comments: true
share: true
---

Apache Beam is a powerful open-source framework for building batch and streaming data processing pipelines. It provides a unified programming model, allowing developers to write data processing logic once and execute it across various data processing frameworks such as Apache Spark, Apache Flink, and Google Cloud Dataflow. In this blog post, we will explore how to read and write data in Apache Beam using Java.

## Reading Data

Apache Beam provides various built-in connectors and transforms for reading data from different sources such as files, databases, and message queues. Let's explore a few examples:

### Reading from a Text File

To read data from a text file, we can use the `TextIO` transform. Here's an example of how to read lines from a text file:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.io.TextIO;
import org.apache.beam.sdk.values.PCollection;

// Create a Pipeline object
Pipeline pipeline = Pipeline.create();

// Read lines from a text file
PCollection<String> lines = pipeline.apply(TextIO.read().from("input.txt"));

// Do further processing on the lines PCollection

// Run the pipeline
pipeline.run();
```

### Reading from a Database

To read data from a database, we can use the `JdbcIO` transform. Here's an example of how to read rows from a database table:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.io.jdbc.JdbcIO;
import org.apache.beam.sdk.values.PCollection;
import java.sql.ResultSet;

// Create a Pipeline object
Pipeline pipeline = Pipeline.create();

// Read rows from a database table
PCollection<ResultSet> rows = pipeline.apply(JdbcIO.<ResultSet>read()
    .withDataSourceConfiguration(JdbcIO.DataSourceConfiguration
        .create("driverClassName", "jdbc:postgresql://host:port/database")
        .withUsername("username")
        .withPassword("password"))
    .withQuery("SELECT * FROM table"));

// Do further processing on the rows PCollection

// Run the pipeline
pipeline.run();
```

## Writing Data

Similar to reading data, Apache Beam provides various connectors and transforms for writing data to different destinations. Let's take a look at a couple of examples:

### Writing to a Text File

To write data to a text file, we can use the `TextIO` transform. Here's an example of how to write lines to a text file:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.io.TextIO;
import org.apache.beam.sdk.values.PCollection;

// Create a Pipeline object
Pipeline pipeline = Pipeline.create();

// Create a PCollection with lines
PCollection<String> lines = ...

// Write lines to a text file
lines.apply(TextIO.write().to("output.txt"));

// Run the pipeline
pipeline.run();
```

### Writing to a Database

To write data to a database, we can use the `JdbcIO` transform. Here's an example of how to write rows to a database table:

```java
import org.apache.beam.sdk.Pipeline;
import org.apache.beam.sdk.io.jdbc.JdbcIO;
import org.apache.beam.sdk.values.PCollection;
import java.sql.PreparedStatement;

// Create a Pipeline object
Pipeline pipeline = Pipeline.create();

// Create a PCollection with rows
PCollection<Row> rows = ...

// Write rows to a database table
rows.apply(JdbcIO.<Row>write()
    .withDataSourceConfiguration(JdbcIO.DataSourceConfiguration
        .create("driverClassName", "jdbc:postgresql://host:port/database")
        .withUsername("username")
        .withPassword("password"))
    .withStatement("INSERT INTO table(column1, column2) VALUES (?, ?)")
    .withPreparedStatementSetter((element, statement) -> {
        statement.setString(1, element.getColumn1());
        statement.setInt(2, element.getColumn2());
    }));

// Run the pipeline
pipeline.run();
```

## Conclusion

Apache Beam provides powerful abstractions and transforms for reading and writing data in a unified manner across different data processing frameworks. In this blog post, we learned how to read and write data using Apache Beam in Java. By leveraging the flexibility of Apache Beam, developers can build robust and scalable data processing pipelines that can handle a wide variety of data sources and formats.

#ApacheBeam #Java