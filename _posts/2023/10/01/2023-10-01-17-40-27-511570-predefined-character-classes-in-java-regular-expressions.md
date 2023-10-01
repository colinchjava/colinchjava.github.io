---
layout: post
title: "Predefined character classes in Java regular expressions"
description: " "
date: 2023-10-01
tags: [Java, RegularExpressions]
comments: true
share: true
---

Here are some of the predefined character classes available in Java regular expressions:

1. `\d` - Matches any digit character (equivalent to `[0-9]`).
2. `\D` - Matches any non-digit character (equivalent to `[^0-9]`).
3. `\w` - Matches any word character, which includes alphanumeric characters (equivalent to `[a-zA-Z0-9_]`).
4. `\W` - Matches any non-word character (equivalent to `[^a-zA-Z0-9_]`).
5. `\s` - Matches any whitespace character (equivalent to `[ \t\n\r\f]`).
6. `\S` - Matches any non-whitespace character (equivalent to `[^ \t\n\r\f]`).

These predefined character classes can be used within square brackets `[]` or on their own within a regular expression pattern. For example, to match any lowercase vowel character, you can use the pattern `[aeiou]`, or you can use the shorthand `\w` to match any word character.

Here is an example that demonstrates the use of predefined character classes in Java regular expressions:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class PredefinedCharacterClassesExample {
    public static void main(String[] args) {
        String text = "Hello 123 World!";
        String pattern = "\\d\\s\\w"; // matches a digit followed by a whitespace character followed by a word character

        Pattern compiledPattern = Pattern.compile(pattern);
        Matcher matcher = compiledPattern.matcher(text);

        while (matcher.find()) {
            System.out.println("Match found: " + matcher.group());
        }
    }
}
```

In this example, the pattern `\d\s\w` is used to find a digit character followed by a whitespace character followed by a word character. The output of this program will be `Match found: 3 W`, as it matches the digit `3`, the space, and the character `W`.

By using predefined character classes, you can simplify your regular expressions and make them more readable. These shortcuts are especially useful when working with common character sets such as digits, words, and whitespace. Remember to escape backslashes (`\`) in Java strings by using double backslashes (`\\`) before the predefined character classes.

#Java #RegularExpressions