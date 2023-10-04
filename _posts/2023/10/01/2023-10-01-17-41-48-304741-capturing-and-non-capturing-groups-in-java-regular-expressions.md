---
layout: post
title: "Capturing and non-capturing groups in Java regular expressions"
description: " "
date: 2023-10-01
tags: [regex]
comments: true
share: true
---

Capturing groups are used to extract specific parts of a matched string. When a regex pattern contains parentheses, the part of the input string that matches the pattern inside the parentheses is "captured" and can be accessed later. You can define multiple capturing groups in a pattern, and each group can be referenced by its index.

To create a capturing group in a regex pattern, simply enclose the desired part of the pattern in parentheses. For example, consider the following pattern that captures a date in the format "DD-MM-YYYY":

```java
String pattern = "(\\d{2})-(\\d{2})-(\\d{4})";
```

In this example, the pattern consists of three capturing groups: one for the day, one for the month, and one for the year. To access the captured groups, you can use the `Matcher` class:

```java
String input = "Today's date is 09-12-2022";
Pattern compiledPattern = Pattern.compile(pattern);
Matcher matcher = compiledPattern.matcher(input);

if (matcher.find()) {
    String day = matcher.group(1);
    String month = matcher.group(2);
    String year = matcher.group(3);

    System.out.println("Day: " + day);
    System.out.println("Month: " + month);
    System.out.println("Year: " + year);
}
```

Running this code will output:

```
Day: 09
Month: 12
Year: 2022
```

Non-capturing groups, on the other hand, are used for grouping purposes but do not capture the matched substring. They are useful when you want to apply quantifiers or other operators to a group but don't need to access the captured content. To create a non-capturing group, prepend `?:` to the opening parentheses:

```java
String pattern = "(?:https?://)?(?:www\\.)?example\\.com";
```

In this example, the pattern matches URLs starting with `https?://` or `www.` followed by `example.com`, but only the entire matched URL is captured, not the individual parts.

Using capturing and non-capturing groups in Java regular expressions can greatly enhance your text processing capabilities. By capturing specific parts of matched strings, you can extract and manipulate relevant data, while non-capturing groups allow you to structure complex patterns without the need to access the captured content.

#java #regex