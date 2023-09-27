---
layout: post
title: "Java control flow statements (if-else, switch, loops)"
description: " "
date: 2023-09-27
tags: [JavaProgramming, ControlFlowStatements]
comments: true
share: true
---
---

Java, being a popular and versatile programming language, provides several control flow statements to control the execution flow of a program. In this article, we will explore three essential control flow statements in Java: `if-else`, `switch`, and loops.

## `if-else` Statement
---

The `if-else` statement in Java allows you to execute a block of code based on a specific condition. Here's an example:

```java
int age = 25;

if(age >= 18) {
    System.out.println("You are eligible to vote.");
}
else {
    System.out.println("You are not eligible to vote.");
}
```
In the above code, the `if` condition checks if the `age` variable is greater than or equal to 18. If the condition is true, the code inside the curly braces will be executed. Otherwise, the code inside the `else` block will be executed.

## `switch` Statement
---

The `switch` statement in Java allows you to perform different actions based on different values of a variable. Here's an example:

```java
int dayOfWeek = 3;
String dayName;

switch (dayOfWeek) {
    case 1:
        dayName = "Sunday";
        break;
    case 2:
        dayName = "Monday";
        break;
    case 3:
        dayName = "Tuesday";
        break;
    // handle other cases...
    default:
        dayName = "Invalid day";
        break;
}

System.out.println("Today is " + dayName);
```

In the above code, the value of `dayOfWeek` determines which case will be executed. If it matches a specific case, the corresponding code block will be executed. If none of the cases match, the code in the `default` block will be executed.

## Loops
---

Loops are used to execute a block of code repeatedly until a specified condition is met. Java provides three types of loops: `for`, `while`, and `do-while`. Let's look at each of these in detail.

### `for` Loop
The `for` loop provides a concise way to iterate over a fixed number of times. Here's an example:

```java
for (int i = 1; i <= 5; i++) {
    System.out.println("Count: " + i);
}
```

In the above code, the loop will execute five times, printing the value of `i` each time.

### `while` Loop
The `while` loop repeatedly executes a block of code as long as a specified condition is true. Here's an example:

```java
int count = 0;

while (count < 5) {
    System.out.println("Count: " + count);
    count++;
}
```

In the above code, the loop will continue executing as long as the `count` variable is less than 5.

### `do-while` Loop
The `do-while` loop is similar to the `while` loop, but it ensures that the block of code is executed at least once, even if the condition is false. Here's an example:

```java
int number = 1;

do {
    System.out.println(number);
    number++;
} while (number <= 5);
```

In the above code, the loop will execute at least once, printing the value of `number` and incrementing it until it reaches 5.

---

These control flow statements are fundamental in Java programming and allow you to have greater control over the execution of your code. **#JavaProgramming** **#ControlFlowStatements**