---
layout: post
title: "API additions in the java.time package in Java 12"
description: " "
date: 2023-10-24
tags: []
comments: true
share: true
---

Java 12 introduced several new additions to the `java.time` package, providing developers with more flexibility and functionality when working with dates and times. In this blog post, we will explore some of the new API additions in Java 12.

## 1. New methods in the `java.time.LocalDate` class

The `java.time.LocalDate` class has been enhanced with two new methods to support common date operations.

### a. `isLeapYear()`

The `isLeapYear()` method allows you to check whether a given year is a leap year or not. It returns `true` if the year is a leap year, and `false` otherwise. Here's an example:

```java
int year = 2020;
boolean isLeapYear = LocalDate.ofYearDay(year, 1).isLeapYear();
System.out.println(year + " is a leap year: " + isLeapYear);
```

Output:
```
2020 is a leap year: true
```

### b. `until(Temporal, TemporalUnit)`

The `until(Temporal, TemporalUnit)` method calculates the amount of time between two `LocalDate` objects in terms of the specified `TemporalUnit`. It returns a `long` value representing the difference between the two dates. For example:

```java
LocalDate startDate = LocalDate.of(2022, 1, 1);
LocalDate endDate = LocalDate.of(2022, 12, 31);
long daysDiff = startDate.until(endDate, ChronoUnit.DAYS);
System.out.println("Number of days between " + startDate + " and " + endDate + ": " + daysDiff);
```

Output:
```
Number of days between 2022-01-01 and 2022-12-31: 364
```

## 2. New methods in the `java.time.LocalDateTime` class

The `java.time.LocalDateTime` class has also received some new methods in Java 12.

### a. `truncatedTo(TemporalUnit)`

The `truncatedTo(TemporalUnit)` method allows you to truncate the time part of a `LocalDateTime` object to a specified `TemporalUnit`. This can be useful when you want to remove the time information, leaving only the date part. Here's an example:

```java
LocalDateTime dateTime = LocalDateTime.of(2022, 3, 15, 14, 30, 45);
LocalDateTime truncatedDateTime = dateTime.truncatedTo(ChronoUnit.HOURS);
System.out.println("Truncated date and time: " + truncatedDateTime);
```

Output:
```
Truncated date and time: 2022-03-15T14:00
```

### b. `isAfter()` and `isBefore()`

The `isAfter()` and `isBefore()` methods allow you to compare two `LocalDateTime` objects to check if one is after or before the other. These methods return a boolean value indicating the result of the comparison. Here's an example:

```java
LocalDateTime dateTime1 = LocalDateTime.of(2022, 5, 15, 10, 0, 0);
LocalDateTime dateTime2 = LocalDateTime.of(2022, 5, 15, 12, 0, 0);

boolean isAfter = dateTime2.isAfter(dateTime1);
boolean isBefore = dateTime1.isBefore(dateTime2);

System.out.println("DateTime2 is after DateTime1: " + isAfter);
System.out.println("DateTime1 is before DateTime2: " + isBefore);
```

Output:
```
DateTime2 is after DateTime1: true
DateTime1 is before DateTime2: true
```

## Conclusion

Java 12 introduced some helpful API additions in the `java.time` package, offering improved support for date and time operations. The new methods in `LocalDate` and `LocalDateTime` classes provide convenient ways to handle leap years, calculate differences between dates, truncate time information, and compare dates. These additions enhance the flexibility and functionality of the `java.time` package, making it easier for developers to work with dates and times in Java.

References:
- Java 12 API Documentation: [https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/time/package-summary.html](https://docs.oracle.com/en/java/javase/12/docs/api/java.base/java/time/package-summary.html)
- Java SE 12 Release Notes: [https://www.oracle.com/java/technologies/javase/12-relnote-issues.html](https://www.oracle.com/java/technologies/javase/12-relnote-issues.html)

#java #javatime