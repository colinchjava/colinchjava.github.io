---
layout: post
title: "Extracting email addresses from a string using Java regular expressions"
description: " "
date: 2023-10-01
tags: [regex]
comments: true
share: true
---

In this blog post, we will explore how to extract email addresses from a string in Java using regular expressions. Regular expressions are powerful patterns that can be used to match and extract specific patterns from textual data.

## The regular expression pattern

To extract email addresses from a string, we can use the following regular expression pattern:

```java
String pattern = "\\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}\\b";
```

Let's break down the pattern:

- `\\b`: Matches word boundaries, ensuring that the email address is not part of a larger word.
- `[A-Za-z0-9._%+-]+`: Matches one or more letters, digits, periods, underscores, percentage signs, or plus/minus signs. These are valid characters for the local part of an email address.
- `@`: Matches the @ symbol.
- `[A-Za-z0-9.-]+`: Matches one or more letters, digits, periods, or hyphens. These are valid characters for the domain name part of an email address.
- `\\.`: Matches a period (escaped with a backslash).
- `[A-Za-z]{2,}`: Matches two or more letters. This is the top-level domain of the email address.

## Using the regular expression in Java

To extract email addresses from a string in Java, we can use the `java.util.regex.Pattern` and `java.util.regex.Matcher` classes:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class EmailExtractor {
    public static void main(String[] args) {
        String input = "Lorem ipsum dolor sit amet, consectetur adipiscing elit. " +
                       "Email addresses: info@example.com, john.doe@example.com";
        String pattern = "\\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,}\\b";

        Pattern regexPattern = Pattern.compile(pattern);
        Matcher matcher = regexPattern.matcher(input);

        while (matcher.find()) {
            String email = matcher.group();
            System.out.println(email);
        }
    }
}
```

In this example, we define a sample input string that contains two email addresses. We compile the regular expression pattern into a `Pattern` object using `Pattern.compile()`. We then create a `Matcher` object using `matcher()`, passing in the input string.

We use the `find()` method of the `Matcher` object to find matches in the input string. For each match, we retrieve the email address using `group()` and print it.

## Conclusion

Regular expressions provide a powerful way to extract email addresses from a string in Java. By using the regular expression pattern we discussed and the `Pattern` and `Matcher` classes provided by Java, extracting email addresses becomes a relatively simple task.

#java #regex