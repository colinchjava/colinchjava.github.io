---
layout: post
title: "Writing in ISO-8859-5 encoding in Java"
description: " "
date: 2023-09-22
tags: [Java, CharacterEncoding]
comments: true
share: true
---

To write text files in the ISO-8859-5 encoding, we will use the `OutputStreamWriter` class in Java's `java.io` package. Here's an example code snippet that demonstrates this:

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStreamWriter;
import java.nio.charset.Charset;

public class ISO88595Writer {
    public static void main(String[] args) {
        String filePath = "path/to/output/file.txt";
        String content = "Привет, мир!"; // Russian text
        
        try (FileOutputStream fos = new FileOutputStream(filePath);
             OutputStreamWriter writer = new OutputStreamWriter(fos, Charset.forName("ISO-8859-5"))) {

            writer.write(content);
            writer.flush();
            System.out.println("File written successfully!");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In the above code, we create a `FileOutputStream` to write the content to a file specified by `filePath`. We then create an `OutputStreamWriter` and pass the `FileOutputStream` object as well as the `Charset` object for "ISO-8859-5" encoding. We write the content to the file using the `write` method of the `OutputStreamWriter` and flush it to ensure the content is written properly.

To read text files encoded in ISO-8859-5, we can use the `InputStreamReader` class in a similar manner:

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStreamReader;
import java.nio.charset.Charset;

public class ISO88595Reader {

    public static void main(String[] args) {
        String filePath = "path/to/input/file.txt";

        try (FileInputStream fis = new FileInputStream(filePath);
             InputStreamReader reader = new InputStreamReader(fis, Charset.forName("ISO-8859-5"))) {

            StringBuilder content = new StringBuilder();
            char[] buffer = new char[1024];
            int length;

            while ((length = reader.read(buffer)) != -1) {
                content.append(buffer, 0, length);
            }

            System.out.println("File content: " + content.toString());

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In the above code, we create a `FileInputStream` to read the file specified by `filePath`. We then create an `InputStreamReader` and pass the `FileInputStream` object as well as the `Charset` object for "ISO-8859-5" encoding. We read the content from the file using the `read` method of the `InputStreamReader` and append it to a `StringBuilder`.

Using the above code snippets, you can easily write and read text files in the ISO-8859-5 encoding in Java. This can be useful when dealing with Cyrillic alphabets or when working with systems that require the ISO-8859-5 encoding.

#Java #CharacterEncoding