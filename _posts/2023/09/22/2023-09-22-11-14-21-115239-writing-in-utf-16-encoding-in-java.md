---
layout: post
title: "Writing in UTF-16 encoding in Java"
description: " "
date: 2023-09-22
tags: [UTF16]
comments: true
share: true
---

UTF-16 is a character encoding scheme that represents each Unicode character with either one or two 16-bit code units. Java provides built-in support for UTF-16 encoding through its `java.nio.charset` package. In this blog post, we will explore how to write text in UTF-16 encoding using Java.

### Writing Text in UTF-16

To write text in UTF-16 encoding in Java, you need to take the following steps:

1. Create a byte stream that represents the desired output location, such as a file or an output stream.
2. Wrap the byte stream with a `OutputStreamWriter` to convert the bytes to characters using the UTF-16 encoding.
3. Use the `write()` method of the `OutputStreamWriter` to write the desired text.

Here is an example of writing a UTF-16 encoded text to a file in Java:

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.nio.charset.StandardCharsets;

public class Utf16WriterExample {
    public static void main(String[] args) {
        String textToWrite = "Hello, World! 你好，世界!";
        String outputFile = "output.txt";

        try (OutputStream outputStream = new FileOutputStream(outputFile);
             OutputStreamWriter writer = new OutputStreamWriter(outputStream, StandardCharsets.UTF_16)) {
            writer.write(textToWrite);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, we create a `FileOutputStream` to represent the output file, and then wrap it with an `OutputStreamWriter` that uses UTF-16 encoding. We then use the `write()` method to write the desired text.

### Conclusion

In this blog post, we learned how to write text in UTF-16 encoding using Java. By following the provided steps and using the appropriate classes from the `java.nio.charset` package, you can easily write Unicode text in UTF-16 encoding in your Java applications.

#java #UTF16