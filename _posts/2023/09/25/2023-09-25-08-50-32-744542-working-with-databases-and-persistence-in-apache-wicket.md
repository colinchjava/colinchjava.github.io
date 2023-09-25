---
layout: post
title: "Working with databases and persistence in Apache Wicket"
description: " "
date: 2023-09-25
tags: [webdevelopment, javawebframework]
comments: true
share: true
---

## Connecting to a Database

To connect Apache Wicket with a database, we need to configure a connection pool and a data source. We will be using Apache Tomcat as our web server, but the process is similar for other servers as well.

1. First, we need to include the database driver JAR file in our project's `lib` folder. This JAR file provides the necessary classes to establish a connection to the database.

2. Next, we need to configure the connection pool and data source in the Tomcat server. This can be done by modifying the `context.xml` file located in the Tomcat installation directory.

    ```xml
    <Context>
        <Resource name="jdbc/mydb"
                  auth="Container"
                  type="javax.sql.DataSource"
                  username="username"
                  password="password"
                  driverClassName="com.mysql.jdbc.Driver"
                  url="jdbc:mysql://localhost:3306/mydb" />
    </Context>
    ```

    Replace `username`, `password`, `driverClassName`, and `url` with the appropriate values for your database.

3. In your Wicket application, create a class that extends `org.apache.wicket.protocol.http.WebApplication` and override the `init()` method.

4. Inside the `init()` method, configure the database connection:

    ```java
    ResourceReference resourceRef = new ResourceReference(DATABASE_NAME) {
        @Override
        protected Resource newResource() {
            return new JdbcConnectionResource(DATABASE_NAME);
        }
    };
    getResourceSettings().addResourceReference(resourceRef);
    ```

    Replace `DATABASE_NAME` with the name you want to give to your database connection.

## Persisting Data

Once the database connection is established, we can start persisting data. Apache Wicket provides several options for this, including using an object-relational mapping (ORM) framework like Hibernate or using raw SQL queries.

### Using an ORM framework

Using an ORM framework like Hibernate can simplify the process of mapping Java objects to database tables. Here is an example of how to use Hibernate in Apache Wicket:

1. First, include the necessary Hibernate dependencies in your project's `pom.xml` file.

    ```xml
    <dependency>
        <groupId>org.hibernate</groupId>
        <artifactId>hibernate-core</artifactId>
        <version>5.4.32.Final</version>
    </dependency>
    ```

2. Configure Hibernate by creating a `hibernate.cfg.xml` file in the `src/main/resources` directory:

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <!DOCTYPE hibernate-configuration PUBLIC
            "-//Hibernate/Hibernate Configuration DTD//EN"
            "http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
    <hibernate-configuration>
        <session-factory>
            <!-- Database connection settings -->
            <property name="hibernate.connection.datasource">java:comp/env/jdbc/mydb</property>
    
            <!-- Specify mapping files -->
            <mapping class="com.example.User" />
        </session-factory>
    </hibernate-configuration>
    ```

3. Create a Java class representing the entity to be persisted. For example, let's create a `User` class:

    ```java
    @Entity
    @Table(name = "users")
    public class User {
        @Id
        @GeneratedValue(strategy = GenerationType.IDENTITY)
        private Long id;
    
        @Column(name = "name")
        private String name;
        
        // getters and setters
    }
    ```

4. In your Wicket application, use Hibernate to save or retrieve data. For example:

    ```java
    SessionFactory sessionFactory = new Configuration().configure().buildSessionFactory();
    Session session = sessionFactory.openSession();
    Transaction transaction = session.beginTransaction();
  
    // Saving a new user
    User user = new User();
    user.setName("John Doe");
    session.save(user);
  
    // Retrieving all users
    CriteriaBuilder criteriaBuilder = session.getCriteriaBuilder();
    CriteriaQuery<User> criteriaQuery = criteriaBuilder.createQuery(User.class);
    criteriaQuery.from(User.class);
    List<User> users = session.createQuery(criteriaQuery).getResultList();
  
    transaction.commit();
    session.close();
    ```

### Using raw SQL queries

If you prefer to use raw SQL queries, Apache Wicket makes it easy to execute them. Here's an example of how to execute a raw SQL query in Apache Wicket:

```java
IDataSourceFactory factory = new SimpleDataSourceFactory(DATABASE_NAME);
JdbcDataProvider<User> provider = new JdbcDataProvider<User>(User.class, "SELECT * FROM users", factory);
List<User> users = provider.getList();
```

Replace `"SELECT * FROM users"` with your own SQL query.

## Conclusion

Working with databases and achieving persistence in Apache Wicket is an essential part of web application development. By configuring the database connection and using either an ORM framework or raw SQL queries, we can efficiently store and retrieve data. Apache Wicket provides flexible options to suit different use cases, making it a popular choice for building robust and scalable web applications.

#webdevelopment #javawebframework