---
layout: post
title: "Matching specific credit card number patterns with Java regular expressions"
description: " "
date: 2023-10-01
tags: [Java, RegularExpressions]
comments: true
share: true
---

Credit card numbers follow a specific format, depending on the type of card. For example, Visa cards have 16 digits, while MasterCard and American Express cards have 15 digits. We can use regular expressions to validate if a given credit card number matches the expected pattern.

To get started, let's define the patterns for each card type using regular expressions:

Visa:
- Pattern: ^4[0-9]{12}(?:[0-9]{3})?$
- Explanation: Starts with 4, followed by 12 digits, with an optional 3-digit extension at the end.

MasterCard:
- Pattern: ^5[1-5][0-9]{14}$
- Explanation: Starts with 5, followed by a digit between 1 and 5, and then 14 additional digits.

American Express:
- Pattern: ^3[47][0-9]{13}$
- Explanation: Starts with 3, followed by either 4 or 7, and then 13 additional digits.

Now that we have defined the patterns, let's see how we can use them in Java:

```java
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class CreditCardValidator {
    public static boolean isValidCreditCard(String cardNumber, String pattern) {
        Pattern regex = Pattern.compile(pattern);
        Matcher matcher = regex.matcher(cardNumber);
        return matcher.matches();
    }

    public static void main(String[] args) {
        String cardNumber = "4111111111111111";
        String visaPattern = "^4[0-9]{12}(?:[0-9]{3})?$";
        boolean isValidVisa = isValidCreditCard(cardNumber, visaPattern);
        System.out.println("Is Visa card valid? " + isValidVisa);

        cardNumber = "5111111111111111";
        String masterCardPattern = "^5[1-5][0-9]{14}$";
        boolean isValidMasterCard = isValidCreditCard(cardNumber, masterCardPattern);
        System.out.println("Is MasterCard valid? " + isValidMasterCard);

        cardNumber = "378282246310005";
        String amexPattern = "^3[47][0-9]{13}$";
        boolean isValidAmex = isValidCreditCard(cardNumber, amexPattern);
        System.out.println("Is American Express valid? " + isValidAmex);
    }
}
```

In the above code, we define a method `isValidCreditCard()` that takes a credit card number and a regular expression pattern as arguments. It returns `true` if the card number matches the pattern, and `false` otherwise.

In the `main()` method, we test the patterns against different credit card numbers and print the validation result.

By using Java regular expressions, we can easily match specific credit card number patterns and validate their format. This can be useful for building secure payment processing systems or implementing credit card validation features in our applications.

#Java #RegularExpressions