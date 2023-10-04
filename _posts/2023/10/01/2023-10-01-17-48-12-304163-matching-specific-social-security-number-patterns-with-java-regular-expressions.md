---
layout: post
title: "Matching specific social security number patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: [RegularExpressions]
comments: true
share: true
---

When working with user data, it is essential to verify that the provided information follows specific patterns. One common example is validating Social Security Numbers (SSNs), which have a well-defined pattern. In this blog post, we will explore how to use Java regular expressions to match specific SSN patterns.

## Understanding the SSN Pattern

In the United States, a Social Security Number typically follows the pattern XXX-XX-XXXX, where X represents a digit. Before applying any regular expressions, it's essential to understand the pattern we need to match:

- The first three digits can range from 001 to 899, excluding 666.
- The next two digits can range from 01 to 99.
- The last four digits can range from 0001 to 9999.

## Using Java Regular Expressions

Java provides the `java.util.regex` package, which includes the `Pattern` and `Matcher` classes to work with regular expressions. Here's an example of using regular expressions to match specific SSN patterns in Java:

```java
import java.util.regex.Pattern;
import java.util.regex.Matcher;

public class SSNValidation {

    private static final String SSN_PATTERN = "^(?!666)(?!000)(\\d{3})-(?!00)(\\d{2})-(?!0000)(\\d{4})$";

    public static boolean isValidSSN(String ssn) {
        Pattern pattern = Pattern.compile(SSN_PATTERN);
        Matcher matcher = pattern.matcher(ssn);
        return matcher.matches();
    }

    public static void main(String[] args) {
        String ssn1 = "123-45-6789";
        String ssn2 = "666-12-3456";
        
        System.out.println("SSN1 is valid: " + isValidSSN(ssn1)); // true
        System.out.println("SSN2 is valid: " + isValidSSN(ssn2)); // false
    }
}
```

In the above example, we define the SSN pattern using the regular expression `"^(?!666)(?!000)(\\d{3})-(?!00)(\\d{2})-(?!0000)(\\d{4})$"`. We use the `Pattern.compile()` method to compile the regular expression and create a `Pattern` object.

The `isValidSSN()` method takes an SSN string as a parameter. It creates a `Matcher` object by invoking the `matcher()` method on the `Pattern` object and passing the SSN string. The `matches()` method is then called on the `Matcher` object to check if the SSN matches the specified pattern.

In the `main()` method, we demonstrate the usage of the `isValidSSN()` method by passing two SSN strings and printing the validation results.

## Conclusion

Regular expressions provide a powerful way to match specific patterns within strings. In the case of Social Security Numbers, using Java regular expressions allows us to validate that the provided SSN follows the expected pattern. By understanding the SSN pattern and leveraging the `Pattern` and `Matcher` classes in Java, we can easily validate SSNs in our applications. Remember to handle user data with care and only collect the necessary information for legitimate purposes.

#Java #RegularExpressions