---
layout: post
title: "How to configure multiple test containers in Arquillian"
description: " "
date: 2023-09-23
tags: [arquillian, testing]
comments: true
share: true
---

Arquillian is a powerful testing framework that allows you to write integration tests for Java-based applications. One of its key features is the ability to run tests in different containers, such as application servers or embedded containers.

In some scenarios, you may need to configure multiple test containers in your Arquillian setup. This could be necessary when testing different parts of your application that require different environments or when you want to run the same tests against multiple containers for comparison purposes.

Here's a step-by-step guide on how to configure multiple test containers in Arquillian:

## 1. Add Dependencies

Make sure you have the necessary dependencies in your project's `pom.xml` file:

```xml
<dependency>
    <groupId>org.jboss.arquillian.junit</groupId>
    <artifactId>arquillian-junit-container</artifactId>
    <version>${arquillian.version}</version>
    <scope>test</scope>
</dependency>
<dependency>
    <!-- Add additional dependencies for other containers here -->
</dependency>
```

Replace `${arquillian.version}` with the desired version of Arquillian.

## 2. Create Arquillian Configuration Files

Create multiple Arquillian configuration files, one for each test container you want to configure. These files should be named using the pattern `arquillian.xml` followed by a specific identifier for the container.

For example, you could have `arquillian-wildfly.xml` for the WildFly application server and `arquillian-tomcat.xml` for the Apache Tomcat container.

```xml
<arquillian xmlns="http://jboss.org/schema/arquillian"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://jboss.org/schema/arquillian http://www.jboss.org/schema/arquillian/arquillian_1_0.xsd">
    <container qualifier="wildfly" default="true">
        <!-- Configuration for WildFly container -->
    </container>
</arquillian>
```

In each configuration file, you can specify the container-specific configuration, such as the target server URL, deployment paths, and any additional settings required.

## 3. Configure Test Classes

In your test classes, you need to specify which test container to use for each test. This can be done by using the `@RunWith` annotation provided by Arquillian along with the desired container adapter.

For example, if you want to run a test using the WildFly container, you would annotate the test class as follows:

```java
@RunWith(Arquillian.class)
@RunAsClient
@ContainerQualifier("wildfly")
public class MyTest {
    // Test methods go here
}
```

Make sure to match the `ContainerQualifier` value with the qualifier specified in the corresponding Arquillian configuration file.

## 4. Run Tests

Finally, you can run your tests using Arquillian's test runner. Arquillian will automatically detect the configured test containers and execute the tests accordingly.

You can use your preferred build tool to run the tests, such as Maven or Gradle, by executing the respective test command.

That's it! You have successfully configured multiple test containers in Arquillian. This allows you to test your application against different runtime environments and compare the results.

#arquillian #testing