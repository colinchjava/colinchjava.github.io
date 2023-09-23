---
layout: post
title: "Using Arquillian with application servers (e.g. WildFly, Tomcat)"
description: " "
date: 2023-09-23
tags: [testing, integrationtesting]
comments: true
share: true
---

## Introduction

Arquillian is a powerful testing framework that allows you to write integration tests for your Java applications. In this blog post, we'll see how to use Arquillian with popular application servers like WildFly and Tomcat.

## What is Arquillian?

Arquillian is a testing framework that simplifies the process of integration testing. It provides a container mechanism that allows you to deploy and test your application in a real or remote environment. Arquillian takes care of starting and stopping the container, deploying the application, and executing the tests within the container.

## Setting Up Arquillian

To use Arquillian with an application server, you need to add the Arquillian dependencies to your project's build file. Let's take a look at how to set up Arquillian for both WildFly and Tomcat.

### Setting Up Arquillian for WildFly

To use Arquillian with WildFly, add the following dependencies to your Maven `pom.xml` file:

```xml
<dependencies>
    <dependency>
        <groupId>org.jboss.arquillian.container</groupId>
        <artifactId>arquillian-wildfly-remote-8.x</artifactId>
        <version>${arquillian.wildfly.version}</version>
        <scope>test</scope>
    </dependency>
    <!-- Other dependencies -->
</dependencies>
```

Replace `${arquillian.wildfly.version}` with the appropriate version of Arquillian for WildFly.

### Setting Up Arquillian for Tomcat

To use Arquillian with Tomcat, add the following dependencies to your Maven `pom.xml` file:

```xml
<dependencies>
    <dependency>
        <groupId>org.jboss.arquillian.container</groupId>
        <artifactId>arquillian-tomcat-embedded-8.x</artifactId>
        <version>${arquillian.tomcat.version}</version>
        <scope>test</scope>
    </dependency>
    <!-- Other dependencies -->
</dependencies>
```

Replace `${arquillian.tomcat.version}` with the appropriate version of Arquillian for Tomcat.

## Writing Arquillian Tests

Once you have set up Arquillian for your application server, you can start writing integration tests. Here's an example of how to write an Arquillian test:

```java
@RunWith(Arquillian.class)
public class MyArquillianTest {

    @Deployment
    public static Archive<?> createDeployment() {
        return ShrinkWrap.create(WebArchive.class)
                .addPackages(true, "com.example")
                .addAsWebInfResource(EmptyAsset.INSTANCE, "beans.xml");
    }

    @Test
    public void testSomething() {
        // Test logic
    }
}
```

In the example above, we are using the `@RunWith` annotation to run the test with Arquillian. The `@Deployment` method is used to create the deployment archive. The `testSomething` method contains the actual test logic.

## Conclusion

Arquillian is a powerful testing framework that simplifies the process of integration testing in Java applications. By following the steps outlined in this blog post, you can easily set up Arquillian with popular application servers like WildFly and Tomcat. Start using Arquillian today and improve the quality and reliability of your integration tests!

#testing #integrationtesting