---
layout: post
title: "Writing in ISO-8859-9 encoding in Java"
description: " "
date: 2023-09-22
tags: [ISO88599]
comments: true
share: true
---

When working with character encodings in Java, it's important to understand how to handle different encodings. In this blog post, we will specifically focus on writing text using the ISO-8859-9 encoding in Java.

## What is ISO-8859-9?

ISO-8859-9, also known as Latin-5, is an 8-bit character encoding that supports the Turkish language. It is an extension of the ISO 8859-1 (Latin-1) encoding, with additional characters needed for Turkish language support, such as the characters "ş" and "ğ".

## Writing Text in ISO-8859-9 Encoding

To write text in ISO-8859-9 encoding in Java, you can use the `OutputStreamWriter` class with a specific encoding as follows:

```java
import java.io.FileOutputStream;
import java.io.OutputStreamWriter;
import java.io.IOException;

public class ISO8859Example {
    public static void main(String[] args) {
        try {
            String text = "Merhaba Dünya!"; // Turkish text to be written
            
            FileOutputStream fos = new FileOutputStream("output.txt");
            OutputStreamWriter osw = new OutputStreamWriter(fos, "ISO-8859-9");
            
            osw.write(text);
            osw.close();
            
            System.out.println("Text written in ISO-8859-9 encoding successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In the example above, we create a `FileOutputStream` to write the text to a file named "output.txt". We then create an `OutputStreamWriter` and specify the encoding as "ISO-8859-9". Finally, we write our Turkish text to the output stream using the `write` method.

Ensure that you handle any potential `IOException` that may occur while writing the text.

## Conclusion

Writing text using the ISO-8859-9 encoding in Java is straightforward using the `OutputStreamWriter` class. By specifying the correct encoding, you can ensure that the output text is properly encoded and can be correctly interpreted by systems or applications that expect ISO-8859-9 encoded text.

Remember to **handle exceptions** properly when working with I/O operations and to follow best practices when dealing with character encodings.

#Java #ISO88599 #Encoding