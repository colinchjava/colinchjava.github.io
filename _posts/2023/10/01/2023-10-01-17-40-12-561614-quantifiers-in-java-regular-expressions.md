---
layout: post
title: "Quantifiers in Java regular expressions"
description: " "
date: 2023-10-01
tags: [regex]
comments: true
share: true
---

Regular expressions (regex) are a powerful tool for pattern matching and text searching in programming languages. Java provides a built-in package called `java.util.regex` that allows you to work with regular expressions. One important aspect of regex in Java is the use of quantifiers. Quantifiers specify how many times a specific pattern needs to occur in the input.

Here are some commonly used quantifiers in Java regular expressions:

## 1. The Asterisk (*) Quantifier 

The asterisk (*) quantifier matches zero or more occurrences of the preceding element. For example, the regex `a*b` will match strings that have zero or more "a" characters followed by a single "b". Let's see an example:

```java
String pattern = "a*b";
String input1 = "b";    // Match: zero occurrences of 'a' followed by a 'b'
String input2 = "ab";   // Match: one occurrence of 'a' followed by a 'b'
String input3 = "aaab"; // Match: multiple occurrences of 'a' followed by a 'b'
String input4 = "bc";   // No match: pattern doesn't end with 'b'
```

## 2. The Plus (+) Quantifier

The plus (+) quantifier matches one or more occurrences of the preceding element. It is similar to the asterisk quantifier, but it requires at least one occurrence. Here's an example:

```java
String pattern = "a+b";
String input1 = "ab";   // Match: one occurrence of 'a' followed by a 'b'
String input2 = "aab";  // Match: multiple occurrences of 'a' followed by a 'b'
String input3 = "b";    // No match: pattern doesn't start with 'a'
String input4 = "ac";   // No match: pattern doesn't end with 'b'
```

## 3. The Question Mark (?) Quantifier

The question mark (?) quantifier matches zero or one occurrence of the preceding element. It makes the preceding element optional. For example, the regex `colou?r` will match either "color" or "colour":

```java
String pattern = "colou?r";
String input1 = "color";   // Match: 'u' is optional
String input2 = "colour";  // Match: includes 'u' in the middle
String input3 = "colr";    // No match: missing 'o' char
String input4 = "colouur"; // No match: excessive 'u'
```

## Conclusion

Quantifiers in Java regular expressions allow you to specify how many times a part of a pattern should occur. The asterisk (*) matches zero or more occurrences, the plus (+) matches one or more occurrences, and the question mark (?) matches zero or one occurrence. Understanding and using these quantifiers can help you create powerful and flexible regex patterns in your Java applications.

#regex #java