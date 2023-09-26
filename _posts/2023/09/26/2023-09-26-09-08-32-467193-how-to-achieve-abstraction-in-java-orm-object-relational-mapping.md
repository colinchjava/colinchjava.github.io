---
layout: post
title: "How to achieve abstraction in Java ORM (object-relational mapping)"
description: " "
date: 2023-09-26
tags: [java, hibernate]
comments: true
share: true
---

When working with a Java ORM (Object-Relational Mapping) framework, abstraction plays a crucial role in achieving separation between the application logic and the underlying database operations. This helps in writing cleaner and more maintainable code. In this blog post, we will explore how to achieve abstraction in Java ORM using an example.

## Understanding Abstraction in ORM

Abstraction in ORM refers to hiding or abstracting away the details of the database and focusing on working with objects and their relationships. Instead of dealing with database queries and low-level database operations, developers can work with objects and let the ORM framework handle the underlying database operations.

## Example: Using Hibernate ORM

Let's take an example of using [Hibernate](https://hibernate.org/) - a popular Java ORM framework - to achieve abstraction.

### Step 1: Setting up Hibernate

First, we need to set up Hibernate in our project. This involves adding the necessary Hibernate dependencies to our project's build file (such as Maven or Gradle). We also need to configure Hibernate with the database connection details in a configuration file.

### Step 2: Defining Entity Classes

Next, we define our entity classes that represent the database tables. These classes typically have fields to represent the table columns and are annotated with Hibernate annotations to map them to the corresponding database tables.

```java
@Entity
@Table(name = "users")
public class User {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "name")
    private String name;
    
    // other fields, getters, and setters
}
```

### Step 3: Interacting with the Database

To interact with the database using Hibernate, we can use the Hibernate Session object. We can create, read, update, or delete data by performing operations on the entity classes.

```java
// Creating a new user
User user = new User();
user.setName("John Doe");

Session session = HibernateUtil.getSessionFactory().openSession();
Transaction transaction = session.beginTransaction();

session.save(user);

transaction.commit();
session.close();

// Retrieving a user by ID
long userId = 1L;

Session session = HibernateUtil.getSessionFactory().openSession();
User user = session.get(User.class, userId);
session.close();

// Updating a user
user.setName("Jane Smith");

Session session = HibernateUtil.getSessionFactory().openSession();
Transaction transaction = session.beginTransaction();

session.update(user);

transaction.commit();
session.close();

// Deleting a user
Session session = HibernateUtil.getSessionFactory().openSession();
Transaction transaction = session.beginTransaction();

session.delete(user);

transaction.commit();
session.close();
```

### Step 4: Abstracting Database Operations

To achieve abstraction, we can create a separate Data Access Object (DAO) class that encapsulates the database operations related to a specific entity. The DAO class provides a higher level of abstraction by exposing methods to interact with the database, abstracting away the details of Hibernate and the underlying database.

```java
public class UserDao {
    public void save(User user) {
        Session session = HibernateUtil.getSessionFactory().openSession();
        Transaction transaction = session.beginTransaction();

        session.save(user);

        transaction.commit();
        session.close();
    }

    public User getById(long id) {
        Session session = HibernateUtil.getSessionFactory().openSession();
        User user = session.get(User.class, id);
        session.close();

        return user;
    }

    // other methods for update, delete, etc.
}
```

With this approach, the application logic can work with the DAO class to perform database operations without knowing the low-level details of Hibernate and the underlying database.

## Conclusion

Achieving abstraction in Java ORM is essential for writing maintainable and scalable applications. By focusing on working with objects and using a proper abstraction layer like DAO classes, we can abstract away the complexities of the database and achieve cleaner and more manageable code.

#java #orm #hibernate #objectrelationalmapping