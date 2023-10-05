---
layout: post
title: "Inserting an element into a Java array"
description: " "
date: 2023-10-05
tags: []
comments: true
share: true
---

Here's an example of how you can insert an element into a Java array:

First, let's say we have an array of integers named `originalArray`:

```java
int[] originalArray = {1, 2, 3, 4, 5};
```

To insert an element, let's say the value `6`, at a specific index, let's say index `2`, we can follow these steps:

1. Create a new array, `newArray`, with a length one greater than the original array:

```java
int[] newArray = new int[originalArray.length + 1];
```

2. Loop through the original array up to the desired index and copy each element to the new array:

```java
for (int i = 0; i < index; i++) {
    newArray[i] = originalArray[i];
}
```

3. Insert the desired element at the desired index:

```java
newArray[index] = element;
```

4. Loop through the remaining elements in the original array, starting from the index, and copy them to the new array, starting from the next index:

```java
for (int i = index; i < originalArray.length; i++) {
    newArray[i + 1] = originalArray[i];
}
```

After executing these steps, the `newArray` will contain the inserted element at the specified index.

Here's the complete code for inserting an element into a Java array:

```java
int[] originalArray = {1, 2, 3, 4, 5};
int index = 2;
int element = 6;

int[] newArray = new int[originalArray.length + 1];
for (int i = 0; i < index; i++) {
    newArray[i] = originalArray[i];
}
newArray[index] = element;
for (int i = index; i < originalArray.length; i++) {
    newArray[i + 1] = originalArray[i];
}

// newArray now contains the inserted element
```

Remember to modify the `index` variable and the `element` variable according to your requirement.

#java #array