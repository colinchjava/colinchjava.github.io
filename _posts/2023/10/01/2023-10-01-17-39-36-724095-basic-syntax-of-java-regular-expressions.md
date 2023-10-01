---
layout: post
title: "Basic syntax of Java regular expressions"
description: " "
date: 2023-10-01
tags: [Java, RegularExpressions]
comments: true
share: true
---

## The Pattern Class

In Java, regular expressions are represented by the `Pattern` class from the `java.util.regex` package. To create a regex pattern, we use the `Pattern.compile()` method, passing the regex string as a parameter. Let's start with some common syntax elements:

1. **Literal Characters**: Ordinary characters like letters, digits, or symbols match themselves exactly. For example, the regex pattern `hello` will match the string "hello" and nothing else.

2. **Metacharacters**: These are special characters with a reserved meaning in regex. Examples of common metacharacters are `.` (matches any character except newline), `*` (matches zero or more occurrences of the preceding element), `+` (matches one or more occurrences), `?` (matches zero or one occurrence), and `\\` (escapes special characters).

3. **Character Classes**: Square brackets `[]` define a character class that matches any one of the characters within it. For example, the regex pattern `[aeiou]` matches any vowel. You can use ranges like `[a-z]` or `[0-9]` to match all lowercase letters or digits respectively.

4. **Predefined Character Classes**: Java provides predefined character classes for common patterns like digits, letters, and whitespace. Some examples are `\\d` (digit), `\\w` (word character), `\\s` (whitespace).

5. **Quantifiers**: Quantifiers define the number of occurrences of the preceding element to match. For instance, `*` matches zero or more occurrences, `+` matches one or more, and `{n}` matches exactly n occurrences.

6. **Anchors**: Anchors define the position of matches within the input string. Examples are `^` (matches the start of the input), `$` (matches the end of the input), and `\\b` (matches a word boundary).

7. **Logical Operators**: We can use logical operators like `|` (OR), `()` (grouping), and `[]` (character class) to create complex regex patterns.

## Example Code

Here's an example that illustrates the basic syntax of Java regular expressions:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class RegexDemo {
    public static void main(String[] args) {
        String input = "Hello, World!";
        String regex = "Hello";

        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(input);

        if (matcher.find()) {
            System.out.println("Match found!");
        } else {
            System.out.println("No match found.");
        }
    }
}
```

In the above code, we create a `Pattern` object by compiling the regex pattern "Hello". We then invoke the `find()` method on the `Matcher` object to search for a match within the input string "Hello, World!". If a match is found, we print "Match found!" otherwise "No match found.".

## Conclusion

Understanding the basic syntax of Java regular expressions is crucial for leveraging the full power of pattern matching and manipulation. By using metacharacters, character classes, quantifiers, anchors, and logical operators, we can create complex regex patterns to match specific patterns within text. By mastering the syntax, you can effectively utilize regex to solve various string manipulation tasks in Java.

#Java #RegularExpressions