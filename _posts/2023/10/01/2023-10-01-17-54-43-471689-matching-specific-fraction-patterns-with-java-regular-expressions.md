---
layout: post
title: "Matching specific fraction patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: [regex]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching and text manipulation. In Java, you can use regular expressions to match specific fraction patterns. This can be useful for tasks such as validating user input or extracting fractions from a string.

Let's take a look at some common fraction patterns and how to match them using Java regular expressions.

## 1. Matching Fractions in the format "numerator/denominator"

To match fractions in the format "numerator/denominator", we can use the following regular expression pattern:

```java
String pattern = "\\d+/\\d+";
```

This pattern consists of two parts:
- `\d+` matches one or more digits for the numerator.
- `\/` matches the forward slash character ("/").
- `\d+` matches one or more digits for the denominator.

Here's an example that demonstrates how to use this pattern to match fractions:

```java
String input = "2/3 4/5 6/7";
String pattern = "\\d+/\\d+";

Pattern regex = Pattern.compile(pattern);
Matcher matcher = regex.matcher(input);

while (matcher.find()) {
    String fraction = matcher.group();
    System.out.println(fraction);
}
```

The output of this example will be:
```
2/3
4/5
6/7
```

## 2. Matching Fractions in the format "whole_number numerator/denominator"

To match fractions in the format "whole_number numerator/denominator", we can use the following regular expression pattern:

```java
String pattern = "\\d+ \\d+/\\d+";
```

This pattern consists of three parts:
- `\d+` matches one or more digits for the whole number.
- ` ` matches the space character.
- `\d+/\\d+` matches the fraction in the same way as before.

Here's an example that demonstrates how to use this pattern:

```java
String input = "1 2/3 2 4/5 3 6/7";
String pattern = "\\d+ \\d+/\\d+";

Pattern regex = Pattern.compile(pattern);
Matcher matcher = regex.matcher(input);

while (matcher.find()) {
    String fraction = matcher.group();
    System.out.println(fraction);
}
```

The output of this example will be:
```
1 2/3
2 4/5
3 6/7
```

## Conclusion

Java regular expressions provide a flexible and powerful way to match specific fraction patterns. By using the appropriate regular expression patterns, you can easily validate and manipulate fraction inputs in your Java applications.

Remember to escape special characters like the forward slash ("/") using double backslashes ("\\") in regular expressions.

#java #regex