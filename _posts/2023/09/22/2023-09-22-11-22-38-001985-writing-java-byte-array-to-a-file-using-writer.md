---
layout: post
title: "Writing Java byte array to a file using Writer"
description: " "
date: 2023-09-22
tags: [FileIO]
comments: true
share: true
---

```java
import java.io.BufferedOutputStream;
import java.io.FileOutputStream;
import java.io.IOException;

public class ByteArrayToFileWriter {

    public static void main(String[] args) {
        byte[] byteArray = { 72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100 }; // Example byte array

        try {
            FileOutputStream fos = new FileOutputStream("output.txt");
            BufferedOutputStream bos = new BufferedOutputStream(fos);

            // Write the byte array to the file
            bos.write(byteArray);

            // Flush and close the streams
            bos.flush();
            bos.close();
            fos.close();

            System.out.println("Byte array successfully written to file!");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In the above code, we create a byte array `byteArray` containing some example bytes. We then create a `FileOutputStream` to write the byte array to a file named "output.txt". We wrap the `FileOutputStream` with a `BufferedOutputStream` to improve performance by adding buffering.

Next, we call the `write` method on the `BufferedOutputStream` and pass in the byte array. This writes the entire byte array to the file.

After writing, we flush and close the streams to ensure that all data is written to the file and resources are properly released.

Finally, we print a success message indicating that the byte array has been successfully written to the file.

By using this code, you will be able to easily write a byte array to a file in Java. Happy coding! #Java #FileIO