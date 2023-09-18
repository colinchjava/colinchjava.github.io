---
layout: post
title: "Working with Java objects and databases with JDBC"
description: " "
date: 2023-09-15
tags: [JDBC]
comments: true
share: true
---

Java Database Connectivity (JDBC) is an API that allows Java programs to interact with relational databases. It provides a set of classes and methods to connect to a database, execute SQL queries, and retrieve results. In this blog post, we will explore how to work with Java objects and databases using JDBC.

## Setting Up the Database

Before we can start working with Java objects and databases, we need to set up a database and create a table to store our data. For this example, let's assume we have a MySQL database with a table named `users`.

We can create the `users` table with the following SQL query:

```sql
CREATE TABLE users (
    id INT PRIMARY KEY,
    name VARCHAR(50),
    email VARCHAR(50)
);
```

## Connecting to the Database

To connect to the database, we first need to load the JDBC driver for the specific database we are using. For MySQL, we can use the following code:

```java
Class.forName("com.mysql.jdbc.Driver");
```

Next, we need to establish a connection to the database by providing the connection URL, username, and password. Here's an example:

```java
String url = "jdbc:mysql://localhost:3306/mydb";
String username = "root";
String password = "password";
Connection connection = DriverManager.getConnection(url, username, password);
```

## Inserting Data

Once we have established a connection to the database, we can start inserting data into the `users` table. We can create a `User` class to represent a user and map it to the table columns.

```java
public class User {
    private int id;
    private String name;
    private String email;
    
    // getters and setters
}
```

To insert a new user into the database, we can use a prepared statement with parameterized queries to prevent SQL injection attacks. Here's an example:

```java
String sql = "INSERT INTO users (id, name, email) VALUES (?, ?, ?)";
PreparedStatement statement = connection.prepareStatement(sql);
statement.setInt(1, user.getId());
statement.setString(2, user.getName());
statement.setString(3, user.getEmail());
statement.executeUpdate();
```

## Retrieving Data

To retrieve data from the database, we can execute a SELECT query and process the results. Here's an example:

```java
String sql = "SELECT * FROM users";
Statement statement = connection.createStatement();
ResultSet resultSet = statement.executeQuery(sql);

while (resultSet.next()) {
    int id = resultSet.getInt("id");
    String name = resultSet.getString("name");
    String email = resultSet.getString("email");
    
    // process the data
}
```

## Closing the Connection

After we are done working with the database, we should close the connection to release any resources. Here's how to do it:

```java
connection.close();
```

That's it! With JDBC, we can easily work with Java objects and databases, execute queries, and retrieve data. It provides a powerful and flexible way to interact with relational databases from Java applications.

#Java #JDBC