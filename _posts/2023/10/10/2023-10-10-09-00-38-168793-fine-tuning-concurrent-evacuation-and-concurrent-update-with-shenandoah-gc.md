---
layout: post
title: "Fine-tuning concurrent evacuation and concurrent update with Shenandoah GC"
description: " "
date: 2023-10-10
tags: []
comments: true
share: true
---

Shenandoah GC is an advanced garbage collector introduced in OpenJDK 12 that focuses on reducing GC pauses and improving overall application performance. It achieves this by performing concurrent garbage collection, meaning it can run in parallel with your application threads, minimizing the impact on application response time.

However, there are situations where you may need to fine-tune the behavior of Shenandoah GC to optimize the concurrent evacuation and concurrent update processes. In this blog post, we will explore some techniques to fine-tune these aspects of Shenandoah GC to further improve its performance.

## 1. Concurrent evacuation

Concurrent evacuation is the process of moving live objects to available free memory regions. By default, Shenandoah GC performs concurrent evacuation in the background, allowing the application threads to continue running.

To fine-tune concurrent evacuation, you can adjust the following parameters:

### a. Concurrent evacuation threads

Shenandoah GC uses multiple threads to parallelize the concurrent evacuation process. By default, it sets the number of threads based on the available CPUs. However, you can manually set the number of threads using the `-XX:ShenandoahConcurrentEvacuationThreads=<number>` flag.

For example, to set the number of concurrent evacuation threads to 4, you can use the following flag:

```
-XX:ShenandoahConcurrentEvacuationThreads=4
```

### b. Concurrent evacuation pacing

Concurrent evacuation pacing controls the speed at which concurrent evacuation processes objects. By default, Shenandoah GC dynamically adjusts the pacing based on the current heap occupancy.

To adjust the pacing, you can use the `-XX:ShenandoahConcurrentEvacuationPacing` flag followed by a value.

For example, to set the concurrent evacuation pacing to 10 milliseconds, you can use the following flag:

```
-XX:ShenandoahConcurrentEvacuationPacing=10ms
```

## 2. Concurrent update

Concurrent update is the process of updating object references and object headers while the application threads are running. Fine-tuning concurrent update can also contribute to improved performance.

To fine-tune concurrent update, you can adjust the following parameters:

### a. Concurrent update threads

Similar to concurrent evacuation, Shenandoah GC utilizes threads to parallelize the concurrent update process. The default number of threads is determined by the available CPUs. However, you can manually set the number of threads using the `-XX:ShenandoahConcurrentUpdateThreads=<number>` flag.

For example, to set the number of concurrent update threads to 2, you can use the following flag:

```
-XX:ShenandoahConcurrentUpdateThreads=2
```

### b. Concurrent update buffer size

Shenandoah GC uses a buffer to store updated object references during the concurrent update process. The buffer size affects the amount of memory allocated for this purpose.

To adjust the buffer size, you can use the `-XX:ShenandoahConcurrentUpdateBuffer=<size>` flag, where `<size>` is specified in bytes.

For example, to set the concurrent update buffer size to 1MB, you can use the following flag:

```
-XX:ShenandoahConcurrentUpdateBuffer=1m
```

## Conclusion

Fine-tuning the concurrent evacuation and concurrent update processes with Shenandoah GC can help optimize garbage collection, thus reducing GC pauses and improving overall application performance. Experimenting with different values for the parameters mentioned above can help you find the optimal settings for your specific workload.

Remember to measure and analyze the impact of these changes on your application's performance before deploying them to production.