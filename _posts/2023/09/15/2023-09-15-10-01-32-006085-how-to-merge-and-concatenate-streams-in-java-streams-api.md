---
layout: post
title: "How to merge and concatenate streams in Java Streams API"
description: " "
date: 2023-09-15
tags: [streaming]
comments: true
share: true
---

Java Streams API provides a powerful and efficient solution for working with collections of data. One common requirement is to merge or concatenate multiple streams into a single stream. In this blog post, we will explore how to accomplish this using the Java Streams API.

## Merging Streams
To merge two or more streams into a single stream, we can make use of the `Stream.concat()` method provided by the `java.util.stream.Stream` class. This method takes two streams as input and returns a new stream that contains all the elements from both input streams.

Here's an example that demonstrates how to merge two streams:

```java
import java.util.stream.Stream;

public class StreamMergeExample {
    public static void main(String[] args) {
        Stream<String> stream1 = Stream.of("apple", "banana", "orange");
        Stream<String> stream2 = Stream.of("kiwi", "mango", "pineapple");

        Stream<String> mergedStream = Stream.concat(stream1, stream2);
        mergedStream.forEach(System.out::println);
    }
}
```
In the above example, we created two streams `stream1` and `stream2` containing some fruits. We then merged these two streams using the `Stream.concat()` method. Finally, we printed all the elements of the merged stream using the `forEach()` method.

## Concatenating Streams
In addition to merging streams, we might also need to concatenate streams, where the elements of the second stream follow the elements of the first stream in the resulting stream.

To concatenate two streams, we can use the `Stream.of()` method along with the `flatMap()` method.

Here's an example that demonstrates how to concatenate two streams:

```java
import java.util.stream.Stream;

public class StreamConcatenateExample {
    public static void main(String[] args) {
        Stream<String> stream1 = Stream.of("Hello", "world");
        Stream<String> stream2 = Stream.of("Java", "Streams");

        Stream<String> concatenatedStream = Stream.of(stream1, stream2)
                .flatMap(stream -> stream);
        concatenatedStream.forEach(System.out::println);
    }
}
```

In the above example, we created two streams `stream1` and `stream2` with some strings. We then concatenated these two streams using the `Stream.of()` method and the `flatMap()` method. Finally, we printed all the elements of the concatenated stream using the `forEach()` method.

With the techniques explained in this blog post, you can easily merge and concatenate streams in Java Streams API, enabling you to efficiently manipulate and process collections of data.

#java #streaming