---
layout: post
title: "Writing in ISO-8859-2 encoding in Java"
description: " "
date: 2023-09-22
tags: [Conclusion]
comments: true
share: true
---

When working with text data in Java, it's important to ensure that the proper character encoding is used to avoid any issues with displaying or manipulating the text. One commonly used character encoding is ISO-8859-2, which is used for Central European languages.

To write text in ISO-8859-2 encoding in Java, you can use the `OutputStreamWriter` class along with the `ISO_8859_2` charset.

Here's an example code snippet that demonstrates how to write text in ISO-8859-2 encoding:

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.nio.charset.Charset;

public class Iso8859_2Writer {
    public static void main(String[] args) {
        String text = "Przykład tekstu w kodowaniu ISO-8859-2";

        try (OutputStreamWriter writer = new OutputStreamWriter(
                new FileOutputStream("output.txt"), Charset.forName("ISO-8859-2"))) {
            writer.write(text);
        } catch (IOException e) {
            System.err.println("Failed to write text to the file: " + e.getMessage());
        }
    }
}
```

In the above code, we first define the text that we want to write in ISO-8859-2 encoding. We then create an instance of `OutputStreamWriter` and specify the output file name along with the `ISO_8859_2` charset. Finally, we use the `write` method of the writer object to write the text to the file.

Remember to handle any potential `IOException` that may occur when writing to the file.

#Conclusion

By using the `OutputStreamWriter` class along with the `ISO_8859_2` charset, you can easily write text in ISO-8859-2 encoding in Java. This ensures that your text is properly encoded and can be correctly read and displayed when needed.
#Java #ISO88592 #CharacterEncoding