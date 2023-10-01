---
layout: post
title: "Adding external libraries to the Java CLASSPATH"
description: " "
date: 2023-10-01
tags: [java, classpath]
comments: true
share: true
---

When working on a Java project, you may need to use external libraries to extend the functionality of your application. These libraries come in the form of JAR (Java Archive) files, which contain pre-compiled Java classes and resources.

To use external libraries in your Java project, you need to add them to the Java CLASSPATH. The CLASSPATH is an environment variable that tells the Java Virtual Machine (JVM) where to find classes and resources when executing your code.

Here are the steps to add external libraries to the Java CLASSPATH:

## 1. Locate the External Library JAR File
First, you need to obtain the JAR file of the external library you want to use. You can either download it directly or include it as a dependency in your project using a dependency management tool like Maven or Gradle.

## 2. Set the CLASSPATH Environment Variable
To add the external library to the CLASSPATH, you can either set the CLASSPATH variable temporarily or permanently.

### Temporary CLASSPATH Setting
Open your terminal or command prompt and navigate to the directory where your Java files are located. Then, use the `java` command with the `-classpath` option to set the CLASSPATH for the current session:

```java
java -classpath /path/to/external/library.jar:. MainClass
```

In this example, replace `/path/to/external/library.jar` with the actual path to the JAR file you want to include. The `:` separates multiple classpath entries, and `.` represents the current directory.

### Permanent CLASSPATH Setting
To set the CLASSPATH permanently, you can modify your system's environment variables.

#### Windows
1. Open the Control Panel and go to System > Advanced system settings.
2. Click on the "Environment Variables" button.
3. In the "System Variables" section, find or create a variable called "CLASSPATH".
4. Add the path to the external library JAR file to the value of the "CLASSPATH" variable, separated by a semicolon (`;`).
5. Click "OK" to save the changes.

#### Unix/Linux
1. Open a terminal and edit the `.bashrc` or `.bash_profile` file in your home directory:
```bash
vi ~/.bashrc
```
2. Add the following line at the end of the file, replacing `/path/to/external/library.jar` with the actual path to the JAR file you want to include:
```bash
export CLASSPATH=/path/to/external/library.jar:.
```
3. Save the file and run the following command to apply the changes:
```bash
source ~/.bashrc
```

## 3. Compile and Run the Java Program
Once the external library is added to the CLASSPATH, you can compile and run your Java program as you normally would, and the JVM will be able to find and use the classes from the external library.

Note that if you're using an IDE like Eclipse or IntelliJ IDEA, they have their own ways of managing libraries and dependencies, so you might not need to manually set the CLASSPATH.

That's it! You have now successfully added an external library to the Java CLASSPATH and can start leveraging its functionality in your Java project.

#java #classpath