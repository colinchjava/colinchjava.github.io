---
layout: post
title: "Matching specific decimal number patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching in Java. They can be used to match specific decimal number patterns as well. In this blog post, we will explore how to use regular expressions in Java to match different decimal number patterns.

1. Matching a decimal number with or without a decimal point:

To match a decimal number with or without a decimal point, we can use the following regular expression:

```java
String regex = "^\\d+(\\.\\d+)?$";
```

Explanation:
- `^` - matches the start of the string
- `\\d+` - matches one or more digits
- `(\\.\\d+)?` - optionally matches a decimal point followed by one or more digits
- `$` - matches the end of the string

Example usage:

```java
String number1 = "123";
String number2 = "3.14";
String number3 = "456.789";

System.out.println(number1.matches(regex)); // true
System.out.println(number2.matches(regex)); // true
System.out.println(number3.matches(regex)); // true
```

2. Matching a decimal number with a specific number of decimal places:

To match a decimal number with a specific number of decimal places, we can use the following regular expression:

```java
String regex = "^\\d+\\.\\d{2}$";
```

Explanation:
- `^` - matches the start of the string
- `\\d+` - matches one or more digits
- `\\.` - matches a decimal point
- `\\d{2}` - matches exactly two digits
- `$` - matches the end of the string

Example usage:

```java
String number1 = "123.45";
String number2 = "3.1415";
String number3 = "456.7";

System.out.println(number1.matches(regex)); // true
System.out.println(number2.matches(regex)); // false
System.out.println(number3.matches(regex)); // false
```

In conclusion, regular expressions in Java can be a powerful tool for matching specific decimal number patterns. Understanding the syntax and using the appropriate regex pattern can help you match decimal numbers with or without decimal points, and even with specific decimal places.