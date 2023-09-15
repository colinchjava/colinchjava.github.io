---
layout: post
title: "Implementing data serialization and deserialization with Java Streams API"
description: " "
date: 2023-09-15
tags: [Java, Serialization, Deserialization]
comments: true
share: true
---

Data serialization is the process of converting an object into a format that can be stored or transmitted, while data deserialization is the reverse process of converting the serialized data back into an object. Java provides the Streams API to help us achieve data serialization and deserialization easily and efficiently. In this blog post, we will explore how to implement data serialization and deserialization using the Java Streams API.

## Serialization

To serialize an object using the Java Streams API, follow these steps:

1. Make sure the class you want to serialize implements the `Serializable` interface. This interface acts as a marker interface, indicating that a class is serializable.

2. Create an instance of the `ObjectOutputStream` class. This class is responsible for writing the serialized data to a stream.

3. Use the `writeObject()` method of the `ObjectOutputStream` class to serialize the object. This method takes the object as a parameter and writes its serialized form to the stream.

4. Close the output stream to release any system resources associated with it.

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;

public class SerializationExample {
    public static void main(String[] args) {
        try (FileOutputStream fileOutputStream = new FileOutputStream("employee.ser");
             ObjectOutputStream objectOutputStream = new ObjectOutputStream(fileOutputStream)) {

            Employee employee = new Employee("John Doe", "Software Engineer", 5000);

            objectOutputStream.writeObject(employee);

            System.out.println("Employee object serialized successfully!");

        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In the above example, we create an instance of the `Employee` class and write it to a file named "employee.ser" using the `ObjectOutputStream`. The `Employee` class must implement the `Serializable` interface for successful serialization.

## Deserialization

To deserialize an object using the Java Streams API, follow these steps:

1. Create an instance of the `ObjectInputStream` class. This class is responsible for reading the serialized data from a stream.

2. Use the `readObject()` method of the `ObjectInputStream` class to deserialize the object. This method reads the serialized form of the object from the stream and returns it.

3. Close the input stream to release any system resources associated with it.

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.ObjectInputStream;

public class DeserializationExample {
    public static void main(String[] args) {
        try (FileInputStream fileInputStream = new FileInputStream("employee.ser");
             ObjectInputStream objectInputStream = new ObjectInputStream(fileInputStream)) {

            Employee employee = (Employee) objectInputStream.readObject();

            System.out.println("Deserialized Employee object: " + employee);

        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

In the above example, we read the serialized form of the `Employee` object from the file "employee.ser" using the `ObjectInputStream`. We then cast the deserialized object to the `Employee` type and print its details.

## Conclusion

The Java Streams API provides a convenient way to perform data serialization and deserialization. By implementing the `Serializable` interface, objects can be easily converted into a serialized format and vice versa. Remember to handle any exceptions that may occur during the serialization and deserialization processes. Start using the Java Streams API for efficient data serialization and deserialization in your Java applications.

#Java #Serialization #Deserialization