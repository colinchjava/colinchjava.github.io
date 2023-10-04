---
layout: post
title: "Matching specific time patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: [RegularExpressions]
comments: true
share: true
---

Regular expressions are a powerful tool used for pattern matching in strings. If you're working with time-related data in Java, you may need to match specific time patterns such as 12-hour or 24-hour time format. In this blog post, we'll explore how to use Java regular expressions to match these time patterns.

## 12-Hour Time Format Matching
To match a time in the 12-hour format (hh:mm AM/PM), you can use the following regular expression:

```java
String regex = "^(0?[1-9]|1[0-2]):[0-5][0-9] (AM|PM)$";
```

Let's break down the regular expression:
- `^` and `$` - The caret (^) and dollar sign ($) are anchors that ensure the entire string matches the pattern.
- `(0?[1-9]|1[0-2])` - This part matches the hours. It allows for either a single digit (0-9) or a two-digit number starting with 1 or 2.
- `:` - Matches the colon character used to separate hours and minutes.
- `[0-5][0-9]` - Matches the minutes. It ensures that minutes are in the range of 00-59.
- `(AM|PM)` - Matches either "AM" or "PM" for the time period.

Here's an example of how to use the regular expression to match a time string:

```java
String time = "08:30 AM";
boolean isMatch = time.matches(regex);
System.out.println("Is it a valid time in 12-hour format? " + isMatch);
```

## 24-Hour Time Format Matching
To match a time in the 24-hour format (hh:mm), you can use the following regular expression:

```java
String regex = "^([01]?[0-9]|2[0-3]):[0-5][0-9]$";
```

Breaking down the regular expression:
- `([01]?[0-9]|2[0-3])` - Matches the hours. It allows for either a single digit (0-9) or a two-digit number starting with 0, 1, or 2.
- `:` - Matches the colon character used to separate hours and minutes.
- `[0-5][0-9]` - Matches the minutes. It ensures that minutes are in the range of 00-59.

Here's an example of using the regular expression to match a time string:

```java
String time = "17:45";
boolean isMatch = time.matches(regex);
System.out.println("Is it a valid time in 24-hour format? " + isMatch);
```

## Conclusion
Java regular expressions provide a flexible way to match specific time patterns. By using the appropriate regular expressions, you can validate whether a given string matches the desired time format, whether it's in 12-hour or 24-hour format. This can be useful when working with time-related data in Java applications.

#Java #RegularExpressions