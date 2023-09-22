---
layout: post
title: "Writing in ISO-8859-1 encoding in Java"
description: " "
date: 2023-09-22
tags: []
comments: true
share: true
---

When working with text in Java, it's important to ensure that you are using the correct character encoding to handle different character sets. One such encoding is ISO-8859-1, also known as Latin-1.

To write text in ISO-8859-1 encoding in Java, you need to pay attention to the encoding used when writing to a file or output stream. Here's an example:

```java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.io.OutputStreamWriter;
import java.nio.charset.StandardCharsets;

public class WriteInISO88591 {

    public static void main(String[] args) {
        try {
            // Create a FileOutputStream with the desired filename
            OutputStream outputStream = new FileOutputStream("output.txt");
            
            // Create an OutputStreamWriter with ISO-8859-1 encoding
            OutputStreamWriter writer = new OutputStreamWriter(outputStream, StandardCharsets.ISO_8859_1);
            
            // Write text in ISO-8859-1 encoding
            String text = "Writing text in ISO-8859-1 encoding";
            writer.write(text);
            
            // Close the writer
            writer.close();
            
            System.out.println("Text written successfully in ISO-8859-1 encoding.");
        } catch (Exception e) {
            System.out.println("Error occurred: " + e.getMessage());
        }
    }
}
```

In the above example, we create a `FileOutputStream` and specify the desired filename, in this case, "output.txt". We then create an `OutputStreamWriter` and pass in the `OutputStream` object along with the desired character encoding, here ISO-8859-1.

We then write the desired text, "Writing text in ISO-8859-1 encoding", using the writer's `write` method. Finally, we close the writer to ensure that all the data is flushed to the file.

Remember to handle any exceptions that may occur during the process.

## Conclusion

Writing in ISO-8859-1 encoding in Java is a straightforward process. By properly setting the encoding when writing to a file or output stream, you can ensure that your text is encoded correctly.