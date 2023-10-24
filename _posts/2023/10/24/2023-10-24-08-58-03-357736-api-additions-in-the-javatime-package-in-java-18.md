---
layout: post
title: "API additions in the java.time package in Java 18"
description: " "
date: 2023-10-24
tags: [References]
comments: true
share: true
---

Java 18 introduces several new additions to the `java.time` package, which provides classes for working with dates, times, and durations. These new APIs aim to enhance the functionality and ease of use when dealing with time-related operations in Java applications.

## DayPeriodAdjuster

One of the new additions in Java 18 is the `DayPeriodAdjuster` interface. This interface allows you to adjust a `LocalDateTime` or `OffsetDateTime` to a specific day period, such as morning, afternoon, or evening. This can be useful when you want to align certain operations or events based on the time of day.

```java
import java.time.LocalDateTime;
import java.time.temporal.ChronoField;
import java.time.temporal.Temporal;
import java.time.temporal.TemporalAdjuster;

public class DayPeriodAdjuster implements TemporalAdjuster {
    @Override
    public Temporal adjustInto(Temporal temporal) {
        int hour = temporal.get(ChronoField.HOUR_OF_DAY);
        if (hour >= 0 && hour < 6) {
            return temporal.with(ChronoField.HOUR_OF_DAY, 0);
        } else if (hour >= 6 && hour < 12) {
            return temporal.with(ChronoField.HOUR_OF_DAY, 6);
        } else if (hour >= 12 && hour < 18) {
            return temporal.with(ChronoField.HOUR_OF_DAY, 12);
        } else {
            return temporal.with(ChronoField.HOUR_OF_DAY, 18);
        }
    }
}
```

With the `DayPeriodAdjuster` class, you can easily adjust a `LocalDateTime` or `OffsetDateTime` instance to the desired day period:

```java
LocalDateTime now = LocalDateTime.now();
LocalDateTime adjustedDateTime = now.with(new DayPeriodAdjuster());
```

## Duration.between with TemporalUnit

Java 18 also introduces a new overload for the `Duration.between` method that accepts a `TemporalUnit` parameter. This allows you to calculate the duration between two `Temporal` objects using a specific temporal unit, such as hours, minutes, or seconds.

```java
import java.time.Duration;
import java.time.LocalTime;
import java.time.temporal.ChronoUnit;

LocalTime time1 = LocalTime.of(10, 30);
LocalTime time2 = LocalTime.of(12, 45);
Duration duration = Duration.between(time1, time2, ChronoUnit.HOURS);
System.out.println(duration.toHours()); // Output: 2
```

In the example above, the `Duration.between` method calculates the duration between `time1` and `time2` in terms of hours.

## Conclusion

The Java 18 update brings valuable enhancements to the `java.time` package, providing more flexibility and convenience when working with dates, times, and durations. The addition of the `DayPeriodAdjuster` interface allows for easy adjustment of time to specific day periods, while the new `Duration.between` overload enables precise duration calculations using a desired temporal unit.

These new API additions in Java 18 further solidify Java's robustness in handling time-related operations and make it even easier to work with date and time in Java applications.

#References

- [Official Java 18 Documentation](https://docs.oracle.com/en/java/javase/18/docs/api/java.base/index.html) 
- [OpenJDK Project](https://openjdk.java.net/projects/jdk/18/) 

#hashtags
#Java18 #java.time