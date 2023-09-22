---
layout: post
title: "Writing in UTF-16LE encoding in Java"
description: " "
date: 2023-09-22
tags: [Encoding]
comments: true
share: true
---

When working with different encodings in Java, it may be necessary to write text in a specific encoding, such as UTF-16LE. In this blog post, we will explore how to write text in UTF-16LE encoding using Java.

### What is UTF-16LE Encoding?

UTF-16LE is a Unicode Transformation Format that uses 16-bit code units. The "LE" stands for Little-Endian, which means that the least significant byte of each 16-bit code unit is stored first.

### Writing Text in UTF-16LE Encoding

To write text in UTF-16LE encoding in Java, you can use the `OutputStreamWriter` class along with the appropriate `Charset` instance. Here is an example code snippet that demonstrates how to do this:

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.io.Writer;
import java.nio.charset.Charset;

public class UTF16LEWriterExample {

    public static void main(String[] args) {
        String text = "Hello, World!";
        Charset utf16le = Charset.forName("UTF-16LE");

        try (FileOutputStream fos = new FileOutputStream("output.txt");
             Writer writer = new OutputStreamWriter(fos, utf16le)) {
            writer.write(text);
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In this example, we create a `Writer` object using the `OutputStreamWriter` class and pass the `FileOutputStream` and `Charset` (UTF-16LE) as arguments. We then simply call the `write()` method on the `Writer` instance to write the text to the file in the specified encoding.

### Conclusion

In this blog post, we have learned how to write text in UTF-16LE encoding using Java. By using the `OutputStreamWriter` class and providing the appropriate `Charset`, we can ensure that the text is written in the desired encoding. Taking care of encoding can be important, especially when working with different systems or formatting requirements.

Remember to always specify the encoding when writing or reading text in Java to ensure that the content is interpreted correctly. 

#Java #Encoding