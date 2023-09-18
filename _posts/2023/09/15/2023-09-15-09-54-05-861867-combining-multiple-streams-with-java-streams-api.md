---
layout: post
title: "Combining multiple streams with Java Streams API"
description: " "
date: 2023-09-15
tags: [StreamsAPI]
comments: true
share: true
---

The Java Streams API provides a powerful and expressive way to process data in a functional and declarative manner. One of its key features is the ability to combine multiple streams into a single stream, enabling you to process data from different sources or apply multiple operations on the same stream. In this blog post, we will explore different ways to combine streams using the Java Streams API.

## Concatenating Streams with `concat()`

The `concat()` method allows you to concatenate two streams into a single stream. It takes two streams as input and returns a new stream that contains all the elements from the first stream followed by all the elements from the second stream.

```java
Stream<Integer> stream1 = Stream.of(1, 2, 3);
Stream<Integer> stream2 = Stream.of(4, 5, 6);

Stream<Integer> combinedStream = Stream.concat(stream1, stream2);
combinedStream.forEach(System.out::println);
```

Output:
```
1
2
3
4
5
6
```

## Merging Streams with `flatMap()`

The `flatMap()` method is another way to combine multiple streams into a single stream. It helps in flattening each element of a stream that contains another stream into a single stream. This is especially useful when you have a stream of collections or arrays and you want to process the elements within those collections/arrays individually.

```java
List<List<Integer>> listOfLists = Arrays.asList(
        Arrays.asList(1, 2, 3),
        Arrays.asList(4, 5, 6),
        Arrays.asList(7, 8, 9)
);

Stream<Integer> combinedStream = listOfLists.stream()
        .flatMap(Collection::stream);

combinedStream.forEach(System.out::println);
```

Output:
```
1
2
3
4
5
6
7
8
9
```

## Joining Streams with `Stream.concat()`

Another way to combine multiple streams is to use the static `Stream.concat()` method. This method takes multiple streams as arguments and returns a new stream that contains all the elements from the input streams.

```java
Stream<Integer> stream1 = Stream.of(1, 2, 3);
Stream<Integer> stream2 = Stream.of(4, 5, 6);
Stream<Integer> stream3 = Stream.of(7, 8, 9);

Stream<Integer> combinedStream = Stream.concat(Stream.concat(stream1, stream2), stream3);
combinedStream.forEach(System.out::println);
```

Output:
```
1
2
3
4
5
6
7
8
9
```

## Conclusion

Combining multiple streams using the Java Streams API allows you to process data from different sources or apply multiple operations on the same stream without the need for intermediary collections. Whether you want to concatenate streams, flatten nested collections, or simply join streams, the Java Streams API provides various methods like `concat()` and `flatMap()` to make this process simple and concise.

#Java #StreamsAPI