---
layout: post
title: "Match floating point numbers with Java regular expressions"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

```java
import java.util.regex.*;

public class Main {
  public static void main(String[] args) {
    String input = "The temperature is 25.6 degrees Celsius.";

    // Regular expression pattern for matching floating point numbers
    Pattern pattern = Pattern.compile("\\d+\\.\\d+");
    Matcher matcher = pattern.matcher(input);

    // Find all matches
    while (matcher.find()) {
      String match = matcher.group();
      System.out.println("Match: " + match);
    }
  }
}
```

In this example, we create a regular expression pattern `"\\d+\\.\\d+"` which matches floating point numbers. This pattern consists of the following components:
- `\\d+` matches one or more digits.
- `\\.` matches the decimal point.
- `\\d+` matches one or more digits after the decimal point.

We then create a `Matcher` object using the input string and the pattern. We can use the `find()` method to find all occurrences of the pattern in the input string. The `group()` method returns the actual matched string.

When you run this code, it will output:
```
Match: 25.6
```

This example demonstrates how to use regular expressions to match floating point numbers in Java.