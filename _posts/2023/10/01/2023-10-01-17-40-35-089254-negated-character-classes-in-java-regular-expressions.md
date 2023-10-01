---
layout: post
title: "Negated character classes in Java regular expressions"
description: " "
date: 2023-10-01
tags: []
comments: true
share: true
---

In Java regular expressions, a negated character class is denoted by the caret symbol (`^`) as the first character inside square brackets (`[]`). It tells the regular expression engine to match any character that is not present in the set specified within the character class.

For example, let's say we want to match any lowercase letter except the vowels (a, e, i, o, u). We can use the following negated character class:

```java
String regex = "[^aeiou]";
```

In this example, the character class `[^aeiou]` will match any single lowercase letter that is not one of the vowels.

Here's a complete code example to demonstrate the use of negated character classes in Java regular expressions:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class NegatedCharacterClassExample {
    public static void main(String[] args) {
        String input = "Hello, world!";
        String regex = "[^aeiou]";

        Pattern pattern = Pattern.compile(regex);
        Matcher matcher = pattern.matcher(input);

        while (matcher.find()) {
            System.out.println("Match: " + matcher.group());
        }
    }
}
```

In this example, we create a `Pattern` object with the regular expression `[^aeiou]`, which represents any character that is not a vowel. We then use a `Matcher` object to find all matches in the input string `"Hello, world!"`. The code will output all the matches, which are the consonants in the string.

Negated character classes are a useful feature in Java regular expressions when you need to match any character except a specific set. By using the caret symbol inside square brackets, you can easily negate a character class and achieve the desired pattern matching behavior.