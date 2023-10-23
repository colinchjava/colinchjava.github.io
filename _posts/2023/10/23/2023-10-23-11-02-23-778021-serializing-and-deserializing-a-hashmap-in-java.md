---
layout: post
title: "Serializing and deserializing a HashMap in Java"
description: " "
date: 2023-10-23
tags: []
comments: true
share: true
---

When working with Java, it's common to need to serialize and deserialize data structures to store and retrieve them from various sources. One such data structure is the HashMap, which allows you to store key-value pairs. In this article, we'll explore how to serialize and deserialize a HashMap in Java.

## Serializing a HashMap

Serializing a HashMap means converting it into a format that can be stored or transmitted, such as a file or a network stream. The process involves converting the HashMap into a byte stream.

To serialize a HashMap in Java, you can make use of the ObjectOutputStream class.

```java
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.ObjectOutputStream;
import java.util.HashMap;

public class HashMapSerializer {

    public static void main(String[] args) {
        HashMap<String, Integer> hashMap = new HashMap<>();
        hashMap.put("Alice", 25);
        hashMap.put("Bob", 30);

        try {
            FileOutputStream fileOut = new FileOutputStream("hashmap.ser");
            ObjectOutputStream out = new ObjectOutputStream(fileOut);
            out.writeObject(hashMap);
            out.close();
            fileOut.close();
            System.out.println("HashMap serialized successfully.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

In the above code, we create a new HashMap and populate it with key-value pairs. We then create an ObjectOutputStream and pass it a FileOutputStream to specify the file where we want to serialize the HashMap. Finally, we call the `writeObject()` method of the ObjectOutputStream to serialize the HashMap.

## Deserializing a HashMap

Deserializing a HashMap means converting it from a byte stream back into its original form, so that it can be used in your Java program.

To deserialize a HashMap in Java, you can make use of the ObjectInputStream class.

```java
import java.io.FileInputStream;
import java.io.IOException;
import java.io.ObjectInputStream;
import java.util.HashMap;

public class HashMapDeserializer {

    public static void main(String[] args) {
        try {
            FileInputStream fileIn = new FileInputStream("hashmap.ser");
            ObjectInputStream in = new ObjectInputStream(fileIn);
            HashMap<String, Integer> hashMap = (HashMap<String, Integer>) in.readObject();
            in.close();
            fileIn.close();
            System.out.println("HashMap deserialized successfully.");
            System.out.println("HashMap: " + hashMap.toString());

        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

In the above code, we create a FileInputStream and pass it the serialized HashMap file. We then create an ObjectInputStream and pass it the FileInputStream. Finally, we call the `readObject()` method of the ObjectInputStream and cast the returned object to the appropriate type (in this case, HashMap<String, Integer>).

## Conclusion

Serialization and deserialization allow you to store and retrieve complex data structures like HashMaps. In this article, we explored how to serialize a HashMap using ObjectOutputStream and how to deserialize it using ObjectInputStream. These techniques can be useful when you need to persist data or transmit it over a network.

# References
- [Java Documentation - ObjectOutputStream](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/io/ObjectOutputStream.html)
- [Java Documentation - ObjectInputStream](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/io/ObjectInputStream.html)