---
layout: post
title: "Checking if two HashMaps are equal in Java"
description: " "
date: 2023-10-23
tags: [References, HashMaps]
comments: true
share: true
---

In Java, `HashMap` is a widely-used class in the `java.util` package, which allows us to store key-value pairs. Often, we may need to compare two `HashMap` objects to see if they are equal. In this blog post, we will explore different ways to accomplish this task.

### Approach 1: Comparing Key-Value Pairs

One way to check if two `HashMap` objects are equal is by comparing their key-value pairs. We can iterate over the entries of each `HashMap` and compare the keys and values one by one.

Here is an example code snippet:

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapComparisonExample {
    public static void main(String[] args) {
        Map<Integer, String> map1 = new HashMap<>();
        map1.put(1, "value1");
        map1.put(2, "value2");

        Map<Integer, String> map2 = new HashMap<>();
        map2.put(1, "value1");
        map2.put(2, "value2");

        boolean isEqual = true;

        if (map1.size() != map2.size()) {
            isEqual = false;
        } else {
            for (Map.Entry<Integer, String> entry : map1.entrySet()) {
                Integer key = entry.getKey();
                String value = entry.getValue();
                if (!map2.containsKey(key) || !map2.get(key).equals(value)) {
                    isEqual = false;
                    break;
                }
            }
        }

        System.out.println("Are the HashMaps equal? " + isEqual);
    }
}
```

In this example, we create two `HashMap` objects, `map1` and `map2`, with the same key-value pairs. We iterate over the entries of `map1`, check if the corresponding key exists in `map2`, and compare the values. If any key-value pair doesn't match or if the sizes of the two maps are different, we set `isEqual` to `false`.

### Approach 2: Using `Equals` Method

Another way to compare two `HashMap` objects for equality is to use the `equals` method provided by the `HashMap` class. This method compares the key-value pairs of two maps and returns `true` if they are equal.

Here is an example code snippet showcasing this approach:

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapComparisonExample {
    public static void main(String[] args) {
        Map<Integer, String> map1 = new HashMap<>();
        map1.put(1, "value1");
        map1.put(2, "value2");

        Map<Integer, String> map2 = new HashMap<>();
        map2.put(1, "value1");
        map2.put(2, "value2");

        boolean isEqual = map1.equals(map2);

        System.out.println("Are the HashMaps equal? " + isEqual);
    }
}
```

In this example, we use the `equals` method to compare `map1` and `map2`. The method internally compares the key-value pairs of both maps, returning `true` if they are equal.

### Conclusion

In this blog post, we explored two different approaches to check if two `HashMap` objects are equal in Java. The first approach involved comparing key-value pairs, while the second approach used the `equals` method provided by the `HashMap` class. Depending on the context and requirements of your application, you can choose the most appropriate approach.

Remember to consider the complexity of your implementation and the runtime performance when comparing large `HashMap` objects.

#References
- [HashMap class in Java](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/HashMap.html)
- [Java Collections Framework](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/util/package-summary.html)

#Java #HashMaps