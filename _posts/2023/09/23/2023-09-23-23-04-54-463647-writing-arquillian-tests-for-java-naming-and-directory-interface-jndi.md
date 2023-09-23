---
layout: post
title: "Writing Arquillian tests for Java Naming and Directory Interface (JNDI)"
description: " "
date: 2023-09-23
tags: [JNDI, Arquillian]
comments: true
share: true
---

In enterprise Java applications, the Java Naming and Directory Interface (JNDI) is commonly used for accessing naming and directory services, such as LDAP or remote EJBs. [Arquillian](https://arquillian.org/) is a powerful testing framework that allows you to write integration tests for JavaEE applications.

In this blog post, we will explore how to write Arquillian tests for JNDI lookup of resources. We will focus on obtaining a JDBC DataSource through JNDI and using it in our tests.

### Setting up the Arquillian environment

To get started, we need to set up the Arquillian environment in our project. Make sure you have the following dependencies in your `pom.xml` file:

```xml
<dependency>
  <groupId>org.jboss.arquillian.junit</groupId>
  <artifactId>arquillian-junit-container</artifactId>
  <version>1.4.0.Final</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>org.jboss.arquillian.container</groupId>
  <artifactId>arquillian-weld-ee-embedded-1.1</artifactId>
  <version>1.4.3.Final</version>
  <scope>test</scope>
</dependency>
```

### Writing the JNDI lookup test

Now, let's write a simple test to perform a JNDI lookup for a JDBC DataSource. Start by creating a new test class and annotate it with `@RunWith(Arquillian.class)`:

```java
@RunWith(Arquillian.class)
public class JndiLookupTest {

    @Deployment
    public static JavaArchive createDeployment() {
        return ShrinkWrap.create(JavaArchive.class)
                .addClass(MyDataSourceProvider.class)
                .addAsManifestResource(EmptyAsset.INSTANCE, "beans.xml");
    }

    @Inject
    private DataSource dataSource;

    @Test
    public void testJndiLookup() {
        Assert.assertNotNull("DataSource not found", dataSource);
        // Perform your tests using the obtained DataSource
    }
}
```

In the above code, we are using the `@Deployment` annotation to create an Arquillian deployment archive. We include `MyDataSourceProvider` class, which is responsible for providing the DataSource implementation, and a `beans.xml` file to activate CDI.

### Implementing the DataSource provider

Next, let's create the `MyDataSourceProvider` class, which will provide a JDBC DataSource through JNDI lookup:

```java
public class MyDataSourceProvider {

    @Produces
    @Resource(mappedName = "java:/jdbc/my-datasource")
    private DataSource dataSource;

    @PostConstruct
    public void setup() {
        // Perform any necessary setup for the DataSource
    }

    @PreDestroy
    public void cleanup() {
        // Perform any necessary cleanup for the DataSource
    }
}
```

In this class, we annotate the `dataSource` field with `@Resource` and specify the `mappedName` as `"java:/jdbc/my-datasource"`. This will perform the JNDI lookup for the specified DataSource.

### Running the Arquillian tests

To run the Arquillian tests, you need to have a compatible Arquillian container configured. You can use containers like WildFly, Payara, or TomEE. You also need to specify the test scope in your `pom.xml` file:

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>3.0.0-M4</version>
      <configuration>
        <testScope>test</testScope>
      </configuration>
    </plugin>
  </plugins>
</build>
```

Now, you can run your Arquillian tests with JUnit, and Arquillian will handle the deployment and execution in the configured container.

#JNDI #Arquillian