---
layout: post
title: "Matching specific ISBN patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: [Regex]
comments: true
share: true
---

When working with International Standard Book Numbers (ISBN), it is often necessary to validate or match specific patterns. ISBNs come in different formats, including ISBN-10 and ISBN-13, and have specific rules for check digits and hyphen placement. In this article, we will explore how to use Java regular expressions to match specific ISBN patterns.

## ISBN-10 Format
The ISBN-10 format consists of ten digits, with the last digit being a check digit. The check digit can be either a digit from 0 to 9 or the letter 'X', which represents 10. The pattern for matching ISBN-10 is as follows:

```java
String isbn10Pattern = "\\b\\d{9}[\\d|X]\\b";
```

This regular expression pattern matches a string that has exactly ten characters, with the last character being either a digit or 'X'. The `\\b` at the beginning and end of the pattern represents word boundaries, ensuring that it matches the whole string and not a part of it.

Here's an example method that uses the ISBN-10 pattern to validate an ISBN:

```java
public boolean validateISBN10(String isbn) {
    String isbn10Pattern = "\\b\\d{9}[\\d|X]\\b";
    return isbn.matches(isbn10Pattern);
}
```

## ISBN-13 Format
The ISBN-13 format consists of thirteen digits, with the last digit being a calculated check digit. The pattern for matching ISBN-13 is as follows:

```java
String isbn13Pattern = "\\b(?=(?:\\d{13}$))\\d{1,5}[-| ]{0,1}\\d{1,7}[-| ]{0,1}\\d{1,6}[-| ]{0,1}[\\d|X]\\b";
```

This regular expression pattern matches a string that has exactly thirteen characters, with hyphens or spaces placed at appropriate positions. The `(?=(?:\\d{13}$))` is a positive lookahead that ensures the string contains exactly thirteen digits. Here again, `\\b` denotes word boundaries.

Here's an example method that uses the ISBN-13 pattern to validate an ISBN:

```java
public boolean validateISBN13(String isbn) {
    String isbn13Pattern = "\\b(?=(?:\\d{13}$))\\d{1,5}[-| ]{0,1}\\d{1,7}[-| ]{0,1}\\d{1,6}[-| ]{0,1}[\\d|X]\\b";
    return isbn.matches(isbn13Pattern);
}
```

## Conclusion
Using regular expressions in Java, you can easily match specific ISBN patterns. Whether you're validating user input or filtering a list of ISBNs, regular expressions offer a powerful and flexible way to handle different ISBN formats. By understanding the patterns and incorporating them into your code, you can ensure the correct formatting and validity of ISBNs.

#Java #Regex