---
layout: post
title: "Using Hazelcast Jet CDC sources in Java applications"
description: " "
date: 2023-09-21
tags: [hashtags, HazelcastJet, CDCSources]
comments: true
share: true
---

In this blog post, we will explore how to use **Hazelcast Jet CDC (Change Data Capture)** sources in Java applications. Change Data Capture is a powerful technique that allows capturing and processing database changes in real time, enabling efficient data integration and synchronization.

## What is Hazelcast Jet CDC?

**Hazelcast Jet CDC** is a module for Hazelcast Jet, an in-memory computing platform that provides high-performance data processing capabilities. The CDC module enables you to capture stream of changes from various databases and integrate with the processing pipelines built with Hazelcast Jet.

## Prerequisites

Before we dive into the integration, let's ensure that you have the following prerequisites:

- Java Development Kit (JDK) installed on your machine
- Maven or Gradle build automation tool installed

## Setting Up the Environment

To get started, you need to set up your development environment with Hazelcast Jet and any desired CDC connector dependencies.

### Maven

Add the following dependencies to your Maven project's `pom.xml` file:

```xml
<dependencies>
    <!-- Hazelcast Jet Core -->
    <dependency>
        <groupId>com.hazelcast.jet</groupId>
        <artifactId>hazelcast-jet-core</artifactId>
        <version>4.5</version>
    </dependency>

    <!-- Hazelcast Jet CDC -->
    <dependency>
        <groupId>com.hazelcast.jet.cdc</groupId>
        <artifactId>hazelcast-jet-cdc-source</artifactId>
        <version>1.0</version>
    </dependency>

    <!-- CDC Connector Dependency (e.g., PostgreSQL) -->
    <dependency>
        <groupId>org.postgresql</groupId>
        <artifactId>postgresql</artifactId>
        <version>42.2.24</version>
    </dependency>
</dependencies>
```

### Gradle

Add the following dependencies to your Gradle project's `build.gradle` file:

```groovy
dependencies {
    // Hazelcast Jet Core
    implementation 'com.hazelcast.jet:hazelcast-jet-core:4.5'

    // Hazelcast Jet CDC
    implementation 'com.hazelcast.jet.cdc:hazelcast-jet-cdc-source:1.0'

    // CDC Connector Dependency (e.g., PostgreSQL)
    implementation 'org.postgresql:postgresql:42.2.24'
}
```

## Using Hazelcast Jet CDC Sources

Once you have set up the environment, you can start utilizing Hazelcast Jet CDC sources in your Java applications.

### Example: Reading from PostgreSQL CDC Source

Here's an example of reading from a CDC source using Hazelcast Jet CDC:

```java
import com.hazelcast.function.FunctionEx;
import com.hazelcast.jet.Jet;
import com.hazelcast.jet.JetInstance;
import com.hazelcast.jet.pipeline.Pipeline;
import com.hazelcast.jet.pipeline.StreamSource;
import com.hazelcast.jet.pipeline.StreamStage;

import java.util.Properties;

public class CDCSourceExample {

    public static void main(String[] args) {
        // Set up Hazelcast Jet instance
        JetInstance jet = Jet.newJetInstance();

        // Set up CDC source properties
        Properties sourceProperties = new Properties();
        sourceProperties.setProperty("database.hostname", "<hostname>");
        sourceProperties.setProperty("database.port", "<port>");
        sourceProperties.setProperty("database.user", "<username>");
        sourceProperties.setProperty("database.password", "<password>");
        sourceProperties.setProperty("database.dbname", "<database>");
        sourceProperties.setProperty("database.schemaname", "<schema>");
        // ... other required properties

        // Create a CDC source
        StreamSource<ChangeRecord> cdcSource = CDCSources.postgres(sourceProperties)
                .setTableWhitelist("<table>")
                .setEmitInitial(true)
                .build();

        // Create a Jet pipeline
        Pipeline pipeline = Pipeline.create();

        // Read from CDC source
        StreamStage<ChangeRecord> cdcStage = pipeline.readFrom(cdcSource);

        // Process the CDC events
        cdcStage.map(FunctionEx.identity())
                .drainTo(Sinks.logger());

        // Submit the pipeline for execution
        jet.newJob(pipeline).join();
    }
}
```

This example demonstrates how to read from a PostgreSQL CDC source using the `CDCSources.postgres()` method. You need to provide the required `database.hostname`, `database.port`, `database.user`, `database.password`, `database.dbname`, and `database.schemaname` properties specific to your database.

Here, we are instructing the CDC source to capture changes from a specific table using `setTableWhitelist()`. Additionally, `setEmitInitial(true)` ensures that the initial snapshot of the table is emitted as well.

Finally, we create a Jet pipeline, read from the CDC source, and process the captured events using various pipeline stages based on your use case.

## Conclusion

Hazelcast Jet CDC sources allow you to effortlessly capture database changes and integrate them with your processing pipelines built with Hazelcast Jet. You can leverage the power of CDC to synchronize data, build real-time analytics applications, and more. Start exploring the Hazelcast Jet CDC module and unlock the potential of change data capture in your Java applications.

#hashtags: #HazelcastJet #CDCSources