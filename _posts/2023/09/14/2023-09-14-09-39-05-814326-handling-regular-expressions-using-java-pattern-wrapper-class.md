---
layout: post
title: "Handling regular expressions using Java Pattern wrapper class"
description: " "
date: 2023-09-14
tags: [RegularExpressions]
comments: true
share: true
---

Regular expressions are a powerful tool for pattern matching and text manipulation in Java. The Java language provides a convenient way to handle regular expressions using the `Pattern` class, which acts as a wrapper around the regular expression syntax.

## Creating a Pattern object

To work with regular expressions, you first need to create a `Pattern` object. The `Pattern` class provides a `compile` method that takes a regular expression as a string and returns a `Pattern` object. For example:

```java
import java.util.regex.Pattern;

Pattern pattern = Pattern.compile("hello");
```

In this example, we have created a `Pattern` object that matches the word "hello".

## Matching a regular expression

Once you have a `Pattern` object, you can use it to match against a given input string. The `Pattern` class provides a `matcher` method that returns a `Matcher` object. The `Matcher` class provides methods to perform various operations on the input string, such as finding matches, extracting groups, and replacing text.

```java
import java.util.regex.Matcher;

String input = "hello world";
Matcher matcher = pattern.matcher(input);

if (matcher.find()) {
    System.out.println("Match found!");
} else {
    System.out.println("No match found.");
}
```

In this example, we create a `Matcher` object by calling the `matcher` method on the `Pattern` object and passing in the input string. We then use the `find` method to check for a match. If a match is found, we print "Match found!", otherwise, we print "No match found."

## Extracting matched groups

Regular expressions often contain groups, which are portions of the pattern enclosed in parentheses. These groups can be extracted from the matched text using the `group` method of the `Matcher` class.

```java
String input = "Hello, my name is John Doe.";
Pattern pattern = Pattern.compile("my name is (.*)\\.");
Matcher matcher = pattern.matcher(input);

if (matcher.find()) {
    String name = matcher.group(1);
    System.out.println("Name: " + name);
}
```

In this example, we have a regular expression that captures the name of a person. By calling the `group` method with an index of `1`, we can extract the contents of the first group.

## Replacing matched text

Regular expressions can also be used to replace portions of a string using the `replaceAll` method of the `Matcher` class.

```java
String input = "Hello world!";
Pattern pattern = Pattern.compile("world");
Matcher matcher = pattern.matcher(input);

String replaced = matcher.replaceAll("Java");
System.out.println("Replaced string: " + replaced);
```

In this example, we replace the word "world" with "Java" using the `replaceAll` method.

# Conclusion

The `Pattern` class in Java provides a convenient way to handle regular expressions. By using the `Matcher` class, you can perform various operations on the input string such as finding matches, extracting groups, and replacing text. Regular expressions are a powerful tool that can greatly enhance your text manipulation capabilities in Java.

**#Java #RegularExpressions**