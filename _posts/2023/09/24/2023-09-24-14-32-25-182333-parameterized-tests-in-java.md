---
layout: post
title: "Parameterized tests in Java"
description: " "
date: 2023-09-24
tags: [Java, JUnit]
comments: true
share: true
---

To write parameterized tests in Java, you can make use of the JUnit framework's `Parameterized` runner. Here's an example:

```java
import org.junit.Test;
import org.junit.runner.RunWith;
import org.junit.runners.Parameterized;
import org.junit.runners.Parameterized.Parameters;

import java.util.Arrays;
import java.util.Collection;

@RunWith(Parameterized.class)
public class MathUtilsTest {
    private final int num1;
    private final int num2;
    private final int expectedResult;

    public MathUtilsTest(int num1, int num2, int expectedResult) {
        this.num1 = num1;
        this.num2 = num2;
        this.expectedResult = expectedResult;
    }

    @Parameters
    public static Collection<Object[]> data() {
        return Arrays.asList(new Object[][] {
                { 2, 3, 5 },
                { -1, 5, 4 },
                { 0, 0, 0 },
                { 10, -5, 5 },
                { 100, 100, 200 }
        });
    }

    @Test
    public void testAddition() {
        int actualResult = MathUtils.add(num1, num2);
        assertEquals(expectedResult, actualResult);
    }
}
```

In this example, the `MathUtilsTest` class is annotated with `@RunWith(Parameterized.class)`, which tells JUnit to use the `Parameterized` runner for executing the tests.

The constructor of the test class takes the input parameters and assigns them to the corresponding instance variables. The parameters are defined as fields in the test class.

The `@Parameters` annotation is used on a static method that returns a collection of parameter arrays. Each parameter array represents a set of input values for the test cases.

The `testAddition` method is the actual test method that will be executed for each set of input parameters. The `assertEquals` assertion is used to validate the expected and actual results.

When the test is run, JUnit will generate separate test instances for each set of input parameters specified in the `data()` method, allowing you to run the same test logic with different inputs.

Using parameterized tests can make your test code more organized and maintainable. It allows you to easily add new test cases without duplicating code, and also provides clear separation of concerns between the test data and the test logic.

#Java #JUnit