---
layout: post
title: "Removing whitespace using Java regular expressions"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

To remove whitespace from a string, you can use the `replaceAll()` function along with the regular expression for whitespace `\\s+`. Here's an example code snippet:

```java
String input = "   Hello     World   ";
String output = input.replaceAll("\\s+", "");

System.out.println(output); // Output: "HelloWorld"
```

In the above code, the `replaceAll()` function replaces all occurrences of one or more whitespace characters with an empty string. The `\\s+` regular expression matches one or more whitespace characters (spaces, tabs, etc.).

You can modify the regular expression as per your requirement. For example, if you only want to remove leading and trailing whitespace, you can use `^\\s+|\\s+$` instead.

Remember to handle null or empty strings appropriately to avoid any exceptions.