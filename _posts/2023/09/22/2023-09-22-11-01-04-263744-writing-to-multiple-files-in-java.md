---
layout: post
title: "Writing to multiple files in Java"
description: " "
date: 2023-09-22
tags: [FileIO]
comments: true
share: true
---

In Java, writing to multiple files can be achieved by using the `FileWriter` class along with a loop to iterate through the files. This approach allows you to write the same data to multiple files without duplicating the code.

## Creating Multiple Files

Before writing to multiple files, you need to create the files first. Here's an example code snippet to create three files named `file1.txt`, `file2.txt`, and `file3.txt`:

```java
import java.io.File;
import java.io.IOException;

public class FileCreationExample {
    public static void main(String[] args) {
        for (int i = 1; i <= 3; i++) {
            File file = new File("file" + i + ".txt");
            try {
                boolean isCreated = file.createNewFile();
                if (isCreated) {
                    System.out.println("File " + file.getName() + " created successfully.");
                } else {
                    System.out.println("File " + file.getName() + " already exists.");
                }
            } catch (IOException e) {
                System.out.println("An error occurred while creating the file: " + e.getMessage());
            }
        }
    }
}
```

In the above example, we iterate from 1 to 3 and create a file with the name `file1.txt`, `file2.txt`, and `file3.txt`, respectively. The `createNewFile()` method creates a new file, and it returns `true` if the file was created successfully or `false` if the file already exists.

## Writing to Multiple Files

Once you have created the files, you can proceed to write data to each file. Here's an example code snippet that demonstrates how to write the same content to multiple files:

```java
import java.io.BufferedWriter;
import java.io.FileWriter;
import java.io.IOException;

public class WriteToMultipleFiles {
    public static void main(String[] args) {
        String content = "Hello, World!";
        for (int i = 1; i <= 3; i++) {
            String filename = "file" + i + ".txt";
            try (BufferedWriter writer = new BufferedWriter(new FileWriter(filename))) {
                writer.write(content);
                System.out.println("Data written to " + filename + " successfully.");
            } catch (IOException e) {
                System.out.println("An error occurred while writing to " + filename + ": " + e.getMessage());
            }
        }
    }
}
```

In the above example, we use a `BufferedWriter` in conjunction with a `FileWriter` to write data to each file. The `BufferedWriter` provides efficient writing by buffering the data, and the `FileWriter` is used to write characters to the file. The `try-with-resources` block ensures that the writer is closed automatically.

By iterating through the files and writing the same content to each one, you can easily write to multiple files using Java.

#Java #FileIO