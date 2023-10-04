---
layout: post
title: "Validating phone numbers with Java regular expressions"
description: " "
date: 2023-10-01
tags: [RegularExpressions]
comments: true
share: true
---

Phone numbers come in various formats depending on the country and the provider. Validating phone numbers is essential to ensure that the provided input is in the correct format. In Java, you can use regular expressions to validate phone numbers.

To validate a phone number in Java using regular expressions, follow these steps:

## Step 1: Create a regular expression pattern

Create a regular expression pattern that matches the desired phone number format. For example, if you want to validate a phone number in the format "+1-123-456-7890", you can use the following pattern:

```java
String pattern = "^\\+[0-9]{1,3}-[0-9]{3}-[0-9]{3}-[0-9]{4}$";
```

## Step 2: Compile the regular expression pattern

Compile the regular expression pattern using the `Pattern` class from the `java.util.regex` package:

```java
Pattern regex = Pattern.compile(pattern);
```

## Step 3: Validate the phone number

Use the compiled regular expression pattern to validate the phone number input string. You can use the `Matcher` class to perform the matching:

```java
String phoneNumber = "+1-123-456-7890";
Matcher matcher = regex.matcher(phoneNumber);

if (matcher.matches()) {
    System.out.println("Valid phone number");
} else {
    System.out.println("Invalid phone number");
}
```

The `matcher.matches()` method returns `true` if the input string matches the regular expression pattern, indicating a valid phone number.

## Example Code:

Here's a complete example that combines all the steps mentioned above to validate a phone number using Java regular expressions:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class PhoneNumberValidator {

    public static boolean validatePhoneNumber(String phoneNumber) {
        String pattern = "^\\+[0-9]{1,3}-[0-9]{3}-[0-9]{3}-[0-9]{4}$";
        Pattern regex = Pattern.compile(pattern);
        Matcher matcher = regex.matcher(phoneNumber);

        return matcher.matches();
    }

    public static void main(String[] args) {
        String phoneNumber = "+1-123-456-7890";
        boolean isValid = validatePhoneNumber(phoneNumber);

        if (isValid) {
            System.out.println("Valid phone number");
        } else {
            System.out.println("Invalid phone number");
        }
    }
}
```

Remember to adapt the regular expression pattern based on the specific phone number format you want to validate.

#Java #RegularExpressions