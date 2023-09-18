---
layout: post
title: "Manipulating files and directories using Java Filesystem wrapper class"
description: " "
date: 2023-09-14
tags: [filesystem, filehandling, javaio]
comments: true
share: true
---

In Java, handling files and directories is a common task when working with file systems. The `java.nio.file` package provides a powerful API for performing file and directory operations. In this blog post, we will explore how to manipulate files and directories using the Java Filesystem wrapper class.

## The Filesystem class

The `java.nio.file.FileSystem` class is an abstract class that serves as a wrapper for a file system. It provides methods for creating, deleting, copying, and moving files and directories.

To access the default filesystem, you can use the `FileSystems` class, which provides static methods for obtaining the default `FileSystem`. Additionally, you can create a new `FileSystem` by calling the `FileSystems.newFileSystem()` method, specifying the path to the file system you want to access.

## Creating a new directory

To create a new directory, you can use the `Files.createDirectory()` method. This method takes a `Path` object representing the directory path and creates the directory in the file system. Here's an example:

```java
import java.nio.file.*;

public class DirectoryExample {
    public static void main(String[] args) throws Exception {
        Path directoryPath = Paths.get("path/to/new/directory");
        Files.createDirectory(directoryPath);
        System.out.println("Directory created successfully!");
    }
}
```

## Creating a new file

To create a new file, you can use the `Files.createFile()` method. This method takes a `Path` object representing the file path and creates the file in the file system. Here's an example:

```java
import java.nio.file.*;

public class FileExample {
    public static void main(String[] args) throws Exception {
        Path filePath = Paths.get("path/to/new/file.txt");
        Files.createFile(filePath);
        System.out.println("File created successfully!");
    }
}
```

## Copying a file

To copy a file, you can use the `Files.copy()` method. This method takes two `Path` objects representing the source and destination file paths and copies the file in the file system. Here's an example:

```java
import java.nio.file.*;

public class CopyExample {
    public static void main(String[] args) throws Exception {
        Path sourcePath = Paths.get("path/to/source/file.txt");
        Path destinationPath = Paths.get("path/to/destination/file.txt");
        Files.copy(sourcePath, destinationPath);
        System.out.println("File copied successfully!");
    }
}
```

## Deleting a file or directory

To delete a file or directory, you can use the `Files.delete()` method. This method takes a `Path` object representing the file or directory path and deletes it from the file system. Here's an example:

```java
import java.nio.file.*;

public class DeleteExample {
    public static void main(String[] args) throws Exception {
        Path path = Paths.get("path/to/file/or/directory");
        Files.delete(path);
        System.out.println("File or directory deleted successfully!");
    }
}
```

## Conclusion

The Java Filesystem wrapper class provides a convenient and straightforward way to manipulate files and directories in Java. By using the `java.nio.file` package and the `FileSystem` class, you can perform various file system operations with ease.

#java #filesystem #filehandling #javaio