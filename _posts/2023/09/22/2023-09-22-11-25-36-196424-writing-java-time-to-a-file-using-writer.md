---
layout: post
title: "Writing Java time to a file using Writer"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

```java
import java.io.FileWriter;
import java.io.IOException;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class TimeWriter {
    public static void main(String[] args) {
        LocalDateTime currentTime = LocalDateTime.now();
        String formattedTime = currentTime.format(DateTimeFormatter.ISO_LOCAL_DATE_TIME);

        try (FileWriter writer = new FileWriter("time.txt")) {
            writer.write(formattedTime);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, we first obtain the current time using `LocalDateTime.now()` and convert it to a string using `format()` method of `DateTimeFormatter` with the `ISO_LOCAL_DATE_TIME` pattern.

Next, we use `FileWriter` to create a writer object and pass the file name `"time.txt"` as the parameter. 

Inside the `try` block, we call the `write()` method of the `writer` object and pass the formatted time string as the parameter to write it to the file.

Finally, we add an exception handling block to catch any `IOException` that may occur during the file writing process.

Remember to handle any exceptions that may occur during file operations to ensure proper error handling.