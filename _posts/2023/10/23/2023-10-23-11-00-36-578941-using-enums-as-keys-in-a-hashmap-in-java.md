---
layout: post
title: "Using enums as keys in a HashMap in Java"
description: " "
date: 2023-10-23
tags: [HashMap]
comments: true
share: true
---

In Java, enums are a powerful and useful feature that allows you to define a set of named constants. They are often used to represent a fixed number of options or choices. One common use case for enums is to serve as keys in a `HashMap`. 

## Enum as HashMap Key

To use an enum as a key in a `HashMap`, you need to ensure that the enum class overrides the `hashCode()` and `equals()` methods. This is necessary because a `HashMap` relies on the `hashCode()` method to determine the bucket where a value should be stored and the `equals()` method to check for key equality when there is a collision.

To illustrate this, let's assume we have an enum called `DaysOfWeek`, which represents the days of the week:

```java
public enum DaysOfWeek {
    MONDAY,
    TUESDAY,
    WEDNESDAY,
    THURSDAY,
    FRIDAY,
    SATURDAY,
    SUNDAY;
}
```

Now, let's create a `HashMap` that uses `DaysOfWeek` as the key and stores some values:

```java
import java.util.HashMap;

public class EnumHashMapExample {
    public static void main(String[] args) {
        HashMap<DaysOfWeek, String> schedule = new HashMap<>();
        
        schedule.put(DaysOfWeek.MONDAY, "Work");
        schedule.put(DaysOfWeek.TUESDAY, "Meeting");
        schedule.put(DaysOfWeek.WEDNESDAY, "Gym");
        
        System.out.println(schedule.get(DaysOfWeek.TUESDAY)); // Output: Meeting
    }
}
```

In this example, we create a `HashMap` called `schedule` where `DaysOfWeek` enums are used as keys and `String` values are associated with each day. We can access the value by using the enum as the key.

## Conclusion

Using enums as keys in a `HashMap` provides a clean and readable way to represent fixed options or choices. By overriding the `hashCode()` and `equals()` methods in the enum class, you can ensure proper behavior when using enums as keys. This approach can enhance code readability and make your code more maintainable.

Remember to handle possible `null` values and ensure thread safety if you are using the `HashMap` in a concurrent environment.

**References:**
- [Java enum documentation](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/lang/Enum.html)
- [Java HashMap documentation](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/HashMap.html)

#Java #HashMap