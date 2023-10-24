---
layout: post
title: "API additions in the java.time package in Java 14"
description: " "
date: 2023-10-24
tags: [datetime]
comments: true
share: true
---

Java 14 introduced several new additions to the `java.time` package, providing developers with more powerful and convenient ways to work with dates, times, and durations. In this blog post, we will explore some of these additions and understand how they can improve our code.

## 1. `DateTimeFormatter.ofLocalizedDate()`

Java 14 introduced the `DateTimeFormatter.ofLocalizedDate()` method, which allows us to format dates based on the user's locale. This is particularly useful when we want to display dates to the user in a localized format, ensuring that it adheres to their regional conventions.

```java
Locale locale = Locale.getDefault();
DateTimeFormatter formatter = DateTimeFormatter.ofLocalizedDate(FormatStyle.MEDIUM).withLocale(locale);
String formattedDate = LocalDate.now().format(formatter);
System.out.println(formattedDate);
```

This code snippet retrieves the default locale, creates a `DateTimeFormatter` with the `MEDIUM` format style, and then formats the current date using this formatter. The resulting formatted date adheres to the user's locale-specific conventions.

## 2. `Duration.between()`

The `Duration.between()` method simplifies the calculation of durations between two instants or temporal objects. It returns a `Duration` object representing the amount of time between the two objects.

```java
LocalDateTime start = LocalDateTime.of(2020, 10, 1, 9, 30);
LocalDateTime end = LocalDateTime.now();
Duration duration = Duration.between(start, end);
System.out.println("Duration: " + duration.toMinutes() + " minutes");
```

In this example, we create two `LocalDateTime` objects representing a start and end time. We then use `Duration.between()` to calculate the duration between these two times. Finally, we retrieve the duration in minutes and print it. This provides an easy way to calculate time intervals accurately.

These are just a few of the API additions in the `java.time` package in Java 14. They demonstrate the ongoing efforts of the Java development team to improve the Java Date and Time API and make it more intuitive and developer-friendly.

For more information on the `java.time` package and its capabilities, refer to the [official Java documentation](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/time/package-summary.html).

Happy coding! :rocket:

#hashtags: #java #datetime