---
layout: post
title: "Applying multiple conditions in Java Streams API filtering"
description: " "
date: 2023-09-15
tags: [StreamsAPI, Filtering]
comments: true
share: true
---

Let's consider a scenario where we have a list of employees and want to filter out the employees who are both senior and have a salary higher than a certain threshold. Here's an example using Java Streams API:

```java
List<Employee> employees = ... // assume we have a list of employees

List<Employee> filteredEmployees = employees.stream()
    .filter(e -> e.getLevel() == Level.SENIOR) // filter by seniority
    .filter(e -> e.getSalary() > 50000) // filter by salary
    .collect(Collectors.toList());
```

In the above example, we start with a stream of employees and first apply the condition to filter by seniority using the `filter()` method. Then, we apply the second condition to filter by salary. Finally, we collect the filtered elements into a new list using the `collect()` method.

Another approach to apply multiple conditions in filtering is to use the `Predicate` functional interface. This allows us to create a more complex condition by combining multiple predicates using logical operators such as AND (`&&`) or OR (`||`). Here's an example:

```java
Predicate<Employee> isSenior = e -> e.getLevel() == Level.SENIOR;
Predicate<Employee> hasHighSalary = e -> e.getSalary() > 50000;

List<Employee> filteredEmployees = employees.stream()
    .filter(isSenior.and(hasHighSalary))
    .collect(Collectors.toList());
```

In this example, we define two `Predicate` instances: `isSenior` and `hasHighSalary`. We then use the `and()` method to combine them into a single predicate that represents the combined condition. Finally, we apply this combined predicate using the `filter()` method.

By using either the chaining of `filter()` methods or the `Predicate` interface, we can easily apply multiple conditions in Java Streams API filtering. This allows us to write more concise and expressive code when dealing with complex filtering scenarios.

#Java #StreamsAPI #Filtering