---
layout: post
title: "Safely performing arithmetic operations using Java BigDecimal wrapper class"
description: " "
date: 2023-09-14
tags: [bigdecimal]
comments: true
share: true
---

Arithmetic operations involving floating-point numbers can sometimes lead to precision errors due to the limitations of the `float` or `double` data types. To avoid such errors, Java provides the `BigDecimal` class, which allows you to perform arithmetic operations with high precision.

## Creating a BigDecimal object

To use the `BigDecimal` class, you need to create an instance of it by passing either a String representation of the number or a `double` value to its constructor. It is recommended to use the `String` constructor to avoid any precision loss during conversion from `double`:

```java
import java.math.BigDecimal;

BigDecimal number1 = new BigDecimal("10.25");
BigDecimal number2 = new BigDecimal("5.75");
```

## Performing arithmetic operations

Once you have created `BigDecimal` objects, you can use them to perform arithmetic operations such as addition, subtraction, multiplication, and division. The `BigDecimal` class provides methods for each of these operations:

### Addition

```java
BigDecimal result = number1.add(number2);
```

### Subtraction

```java
BigDecimal result = number1.subtract(number2);
```

### Multiplication

```java
BigDecimal result = number1.multiply(number2);
```

### Division

```java
BigDecimal result = number1.divide(number2, BigDecimal.ROUND_HALF_UP);
```

Note that when performing division, you need to specify the rounding mode as the second argument to the `divide` method. In this example, we used `BigDecimal.ROUND_HALF_UP` to round the result to the nearest value.

## Handling precision and scale

The `BigDecimal` class allows you to control the precision and scale of your calculations. Precision refers to the total number of digits, while scale refers to the number of digits to the right of the decimal point.

You can specify the precision and scale when creating a `BigDecimal` object:

```java
BigDecimal number = new BigDecimal("10.123456789");
```

Or you can set the precision and scale using the `setScale` method:

```java
BigDecimal result = number.setScale(2, BigDecimal.ROUND_HALF_UP);
```

In this example, `setScale(2)` sets the scale of the `BigDecimal` object to 2, which means it will have two digits to the right of the decimal point. The `ROUND_HALF_UP` rounding mode is used to round the result.

## Conclusion

Using the `BigDecimal` class in Java allows you to safely perform arithmetic operations without the risk of precision errors. It provides precise control over precision and scale, ensuring accurate calculations even when dealing with large numbers or decimal fractions. By consistently using `BigDecimal` for arithmetic operations, you can trust the accuracy of your calculations in your Java applications.

#java #bigdecimal