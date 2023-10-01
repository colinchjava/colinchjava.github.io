---
layout: post
title: "Matching specific phone number patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: [regex, java]
comments: true
share: true
---

Phone numbers come in various formats and it can be quite challenging to match them using traditional string manipulation methods. Luckily, Java provides regular expressions as a powerful tool for pattern matching. In this blog post, we will explore how to use Java regular expressions to match specific phone number patterns.

Let's say we want to match phone numbers in the following formats:
1. (123) 456-7890
2. 123-456-7890
3. 1234567890

To match these formats, we can use the following regular expression pattern: 

```java
String pattern = "\\(?\\d{3}\\)?[-\\s]?\\d{3}[-\\s]?\\d{4}";
```

Let's deconstruct this pattern:
- `\\(?` matches an optional opening parentheses `(`
- `\\d{3}` matches three digits
- `\\)?` matches an optional closing parentheses `)`
- `[-\\s]?` matches an optional hyphen `-` or whitespace character `\s`
- `\\d{3}` matches three digits
- `[-\\s]?` matches an optional hyphen `-` or whitespace character `\\s`
- `\\d{4}` matches four digits

Using this pattern, we can match all three phone number formats.

Here's an example code snippet that demonstrates the usage of the regular expression pattern:

```java
import java.util.regex.*;

public class PhoneNumberMatcher {
   public static void main(String[] args) {
     String phoneNumber1 = "(123) 456-7890";
     String phoneNumber2 = "123-456-7890";
     String phoneNumber3 = "1234567890";
     
     String pattern = "\\(?\\d{3}\\)?[-\\s]?\\d{3}[-\\s]?\\d{4}";
     Pattern compiledPattern = Pattern.compile(pattern);
     
     Matcher matcher1 = compiledPattern.matcher(phoneNumber1);
     Matcher matcher2 = compiledPattern.matcher(phoneNumber2);
     Matcher matcher3 = compiledPattern.matcher(phoneNumber3);
     
     System.out.println("Phone number 1 matches? " + matcher1.matches());
     System.out.println("Phone number 2 matches? " + matcher2.matches());
     System.out.println("Phone number 3 matches? " + matcher3.matches());
   }
}
```
Output:
```
Phone number 1 matches? true
Phone number 2 matches? true
Phone number 3 matches? true
```
In the example code, we compile the regular expression pattern using `Pattern.compile()` method. Then, we create a `Matcher` object for each phone number and use the `matches()` method to check if the phone number matches the pattern.

Regular expressions provide a flexible and powerful way to match complex patterns in strings. By using regular expressions in Java, you can easily match specific phone number patterns and handle various formats efficiently.

#regex #java