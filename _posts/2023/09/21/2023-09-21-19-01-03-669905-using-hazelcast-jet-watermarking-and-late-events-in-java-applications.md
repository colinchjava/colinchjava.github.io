---
layout: post
title: "Using Hazelcast Jet watermarking and late events in Java applications"
description: " "
date: 2023-09-21
tags: [streamprocessing, HazelcastJet]
comments: true
share: true
---

In stream processing applications, it is crucial to handle out-of-order or late arriving events effectively. Hazelcast Jet, a distributed stream processing engine, provides robust support for watermarking and handling late events. Watermarking allows Jet to track the progress of event processing and make informed decisions about handling late events. This blog post will explore how to use watermarking and handle late events in Java applications with Hazelcast Jet.

## What is Watermarking?

Watermarking is a technique used to track the progress of event time in stream processing systems. It represents a timestamp that signifies when the system expects to have received all events with a lower timestamp. Watermarks are typically emitted by a source or a processing stage and are propagated downstream to enable time-based operations such as windowing and event time-based aggregations.

## Setting up Watermarking in Hazelcast Jet

Hazelcast Jet allows easy configuration of watermarking in your pipeline. Here's an example that demonstrates how to set up watermarking in a Jet pipeline:

```java
Pipeline pipeline = Pipeline.create();
pipeline
    .readFrom(Sources.<Event>list("inputList"))
    .withTimestampsAndWatermarks(event -> event.getTimestamp(), new BoundedOutOfOrdernessWatermarkGenerator<>(Time.seconds(5)))
    .map(event -> processEvent(event))
    .writeTo(Sinks.list("outputList"));
```

In the above code, the `withTimestampsAndWatermarks()` method is used to assign timestamps and watermarks to the events. The `event -> event.getTimestamp()` lambda function extracts the timestamp from the event object. The `BoundedOutOfOrdernessWatermarkGenerator` is used to generate watermarks with a specified delay, in this case, 5 seconds.

## Handling Late Events

Hazelcast Jet provides built-in support for handling late events using watermarking. When an event arrives with a timestamp that is earlier than the watermark, it is considered a late event. By default, late events are dropped from processing as they are considered out-of-order. However, Hazelcast Jet allows you to configure custom behavior for handling late events.

To handle late events, you can use the `allowedLateness()` method on the windowed operations. Here's an example that demonstrates handling of late events in a windowed operation:

```java
StreamStage<KeyedWindowResult<Integer, Integer>> windowedStream = pipeline
    .readFrom(Sources.<Event>list("inputList"))
    .withTimestampsAndWatermarks(event -> event.getTimestamp(), new BoundedOutOfOrdernessWatermarkGenerator<>(Time.seconds(5)))
    .window(WindowDefinition.tumbling(Time.seconds(10)))
    .allowedLateness(Time.seconds(60))
    .groupingKey(event -> event.getKey())
    .aggregate(AggregateOperations.summingInt(event -> event.getValue()));
```

In the code above, the `.allowedLateness(Time.seconds(60))` method is used to specify a time duration within which late events will be accepted. After this duration, the late events will be dropped. In this example, any events arriving within 60 seconds after the watermark will be included in the windowed operation.

## Conclusion

Watermarking and handling late events are essential techniques in stream processing applications. With Hazelcast Jet, you can easily configure and utilize watermarking to track event time and handle late arrivals efficiently. By using the `withTimestampsAndWatermarks()` and `allowedLateness()` methods, you can ensure accurate processing of out-of-order or late arriving events. Incorporate these features in your stream processing pipelines to build robust and reliable applications.

#streamprocessing #HazelcastJet