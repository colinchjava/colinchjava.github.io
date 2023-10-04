---
layout: post
title: "Matching specific currency patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: [RegularExpressions]
comments: true
share: true
---

To match currency patterns using regular expressions, you can create a regular expression pattern that matches the desired currency format. Here's an example of how you can do it in Java:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class CurrencyMatcher {
    public static void main(String[] args) {
        String input = "The price is $10.99";
        String pattern = "\\$\\d+(\\.\\d{2})?";

        Pattern regexPattern = Pattern.compile(pattern);
        Matcher matcher = regexPattern.matcher(input);

        while (matcher.find()) {
            String match = matcher.group();
            System.out.println("Found currency: " + match);
        }
    }
}
```

In this example, we have a sample input string "The price is $10.99" and we want to extract the currency value "$10.99" from it. The regular expression pattern "\\$\\d+(\\.\\d{2})?" is used to match the currency pattern.

Let's break down the regular expression pattern:
- "\\$" matches the dollar sign character.
- "\\d+" matches one or more digits.
- "(\\.\\d{2})?" matches an optional decimal part consisting of a dot followed by exactly two digits.

When we run the above code, it will output:
```
Found currency: $10.99
```

This demonstrates how to use regular expressions in Java to match and extract specific currency patterns from a string. You can modify the pattern to match different currency formats or add additional logic to handle more complex scenarios.

#Java #RegularExpressions