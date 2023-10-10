---
layout: post
title: "Fine-tuning concurrent marking stats and concurrent phase termination with Shenandoah GC"
description: " "
date: 2023-10-10
tags: [ShenandoahGC, GarbageCollector]
comments: true
share: true
---

![Shenandoah GC](shenandoah_gc.jpg)

Shenandoah GC is a low-pause garbage collector introduced in JDK 12 that aims to reduce GC pause times for large heaps. It achieves this by performing concurrent phases for major GC cycles, allowing the application to continue running while garbage collection is in progress.

In this blog post, we will explore two fine-tuning techniques for Shenandoah GC - concurrent marking stats and concurrent phase termination. These techniques can help improve performance and reduce pause times further.

## Concurrent Marking Stats

Concurrent marking is the phase where the GC marks all live objects in the heap. Shenandoah GC splits this phase into multiple concurrent marking cycles to minimize the pause times. During each marking cycle, a certain amount of work is performed, and then the GC thread yields to the application threads.

To fine-tune the concurrent marking behavior, Shenandoah GC provides several options related to marking stats. These options control the behavior of the GC when it comes to deciding how much work to perform in each cycle.

The most important option is `ShenandoahMarkRefProcFrequency`, which specifies the number of references processed per cycle. By default, 10% of all references are processed in each cycle. However, this value can be adjusted based on the application's characteristics.

To increase the amount of work done per cycle, set a higher value for `ShenandoahMarkRefProcFrequency`. For example, setting it to 30% will result in more work being done in each cycle, potentially reducing the overall marking time.

Another option is `ShenandoahConcMarkCycles`, which determines the number of concurrent marking cycles to perform. Increasing this value can distribute the marking work over more cycles, reducing the load on the GC thread and minimizing pauses.

## Concurrent Phase Termination

Concurrent phase termination is another technique that can be fine-tuned in Shenandoah GC. During the concurrent marking phase, the GC thread interacts with application threads to ensure that all objects are correctly marked. Once all objects are marked, the GC thread can terminate the marking phase and proceed to the next phase.

Shenandoah GC provides the option `ShenandoahConcurrency`, which controls how aggressively the GC thread checks for termination. By default, the GC thread checks for termination every 10 milliseconds. However, this value can be adjusted depending on the application's requirements.

To reduce the termination check interval, set a lower value for `ShenandoahConcurrency`. This will cause the GC thread to check for termination more frequently, potentially reducing the marking phase's duration and overall pause time.

## Conclusion

Fine-tuning concurrent marking stats and concurrent phase termination in Shenandoah GC can help optimize garbage collection behavior and further reduce pause times. By adjusting the marking stats and termination check interval, developers can align the GC behavior more closely with their application's requirements, leading to improved performance.

Remember to experiment with different values and monitor the impact on your application's performance and pause times. Fine-tuning GC parameters can be a trial-and-error process, so it's important to measure and analyze the results.

### #ShenandoahGC #GarbageCollector