---
layout: post
title: "Writing to a file using PipedWriter in Java"
description: " "
date: 2023-09-22
tags: [fileio]
comments: true
share: true
---

In Java, the `PipedWriter` class is used to write data into a *pipe*. A pipe is a communication channel that connects two threads: one for writing and another for reading. This allows for easy communication between threads in a Java program.

Here's an example code that demonstrates how to use `PipedWriter` to write data into a file:

```java
import java.io.*;

public class FileWriterExample {
    public static void main(String[] args) {
        try {
            // Create a PipedWriter and connect it to a PipedReader
            PipedWriter writer = new PipedWriter();
            PipedReader reader = new PipedReader(writer);
            
            // Create a BufferedWriter for writing into a file
            BufferedWriter fileWriter = new BufferedWriter(new FileWriter("output.txt"));

            // Create a separate thread to read from the pipe and write to the file
            Thread readerThread = new Thread(new Runnable() {
                @Override
                public void run() {
                    try {
                        int data;
                        while ((data = reader.read()) != -1) {   // Read from the pipe
                            fileWriter.write(data);   // Write to the file
                            fileWriter.flush();
                        }
                        fileWriter.close();
                    } catch (IOException e) {
                        e.printStackTrace();
                    }
                }
            });

            readerThread.start();

            // Write some data to the pipe
            writer.write("Hello, World!");

            // Close the writer to signal the end of data
            writer.close();

            // Wait for the reader thread to finish
            readerThread.join();
        } catch (IOException | InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

In the code above, we first create a `PipedWriter` and connect it to a `PipedReader`. Then, we create a `BufferedWriter` that writes data into a file named "output.txt". 

We then create a separate thread that continuously reads from the pipe using the `PipedReader` and writes the data into the file using the `BufferedWriter`. The main thread writes the data "Hello, World!" into the pipe using the `write()` method of `PipedWriter`.

Finally, we close the `PipedWriter` to indicate that no more data will be written, and wait for the reader thread to finish before exiting the program.

That's it! Now you know how to use `PipedWriter` to write data into a file in Java. Try running the code and check the "output.txt" file to see the result.

#java #fileio