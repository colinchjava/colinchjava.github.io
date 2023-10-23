---
layout: post
title: "Sorting a HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

In Java, the HashMap class does not guarantee any specific order of its elements. However, in some cases, it may be necessary to sort the elements of a HashMap based on their keys or values. This article will explain how to sort a HashMap in Java.

## Sorting by Keys

To sort a HashMap by keys, we need to extract the keys and sort them using a predefined comparator. We can then use the sorted keys to access the corresponding values from the HashMap.

Here's an example:

```java
import java.util.*;

public class HashMapSortByKeyExample {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("John", 23);
        map.put("Alice", 30);
        map.put("Bob", 27);

        List<String> sortedKeys = new ArrayList<>(map.keySet());
        Collections.sort(sortedKeys);

        for (String key : sortedKeys) {
            System.out.println("Key: " + key + ", Value: " + map.get(key));
        }
    }
}
```

In this example, we create a HashMap called `map` with string keys and integer values. We then use the `keySet()` method to extract a set of keys from the HashMap and convert it into an ArrayList. Finally, we sort the ArrayList using `Collections.sort()` and iterate over the sorted keys to access the corresponding values.

The output will be:

```
Key: Alice, Value: 30
Key: Bob, Value: 27
Key: John, Value: 23
```

## Sorting by Values

To sort a HashMap by values, we need to extract the entries of the HashMap into a list of Map.Entry objects. We can then sort the list using a custom comparator based on the values of the entries.

Here's an example:

```java
import java.util.*;

public class HashMapSortByValueExample {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("John", 23);
        map.put("Alice", 30);
        map.put("Bob", 27);

        List<Map.Entry<String, Integer>> sortedEntries = new ArrayList<>(map.entrySet());
        Collections.sort(sortedEntries, new Comparator<Map.Entry<String, Integer>>() {
            public int compare(Map.Entry<String, Integer> entry1, Map.Entry<String, Integer> entry2) {
                return entry1.getValue().compareTo(entry2.getValue());
            }
        });

        for (Map.Entry<String, Integer> entry : sortedEntries) {
            System.out.println("Key: " + entry.getKey() + ", Value: " + entry.getValue());
        }
    }
}
```

In this example, we create a HashMap called `map` with string keys and integer values. We then use the `entrySet()` method to obtain a set of Map.Entry objects representing the key-value pairs of the HashMap. We convert this set into an ArrayList and sort it using a custom comparator that compares the values of the entries.

The output will be:

```
Key: John, Value: 23
Key: Bob, Value: 27
Key: Alice, Value: 30
```

By following these approaches, you can easily sort a HashMap in Java based on keys or values. This can be useful in scenarios where the ordering of the elements is important for further processing or presentation.

For more information on sorting HashMaps and other collections in Java, refer to the [Java documentation](https://docs.oracle.com/en/java/javase/14/docs/api/java.base/java/util/HashMap.html).