---
layout: post
title: "Implementing remote interfaces in Java RMI"
description: " "
date: 2023-09-14
tags: []
comments: true
share: true
---

Remote Method Invocation (RMI) is a Java technology that allows objects residing in one Java Virtual Machine (JVM) to invoke methods on objects residing in another JVM. It is a powerful mechanism for building distributed applications in Java.

One of the key components of RMI is the use of remote interfaces. Remote interfaces define the methods that can be accessed remotely by clients. In this blog post, we will explore how to implement remote interfaces in Java RMI.

## Step 1: Define the remote interface

First, we need to define the remote interface that will be implemented by the remote object. The remote interface should extend the `Remote` interface and all the methods declared in the interface must throw the `RemoteException` in case of any remote invocation error.

```java
import java.rmi.Remote;
import java.rmi.RemoteException;

public interface SampleRemoteInterface extends Remote {
    void sayHello() throws RemoteException;

    int add(int a, int b) throws RemoteException;
}
```

In the above example, we have defined a remote interface `SampleRemoteInterface` that declares two methods `sayHello` and `add`. Both methods are declared to throw `RemoteException`.

## Step 2: Implement the remote interface

Next, we need to implement the remote interface on a class that will act as the remote object. This class should extend the `UnicastRemoteObject` class and must provide an implementation for all the methods declared in the remote interface.

```java
import java.rmi.RemoteException;
import java.rmi.server.UnicastRemoteObject;

public class SampleRemoteObject extends UnicastRemoteObject implements SampleRemoteInterface {
    public SampleRemoteObject() throws RemoteException {
        // Required default constructor
    }

    @Override
    public void sayHello() throws RemoteException {
        System.out.println("Hello from the remote object!");
    }

    @Override
    public int add(int a, int b) throws RemoteException {
        return a + b;
    }
}
```

In the above example, we have implemented the `SampleRemoteInterface` on the `SampleRemoteObject` class. It extends the `UnicastRemoteObject` class and provides implementations for the `sayHello` and `add` methods.

## Step 3: Create and start the RMI server

To make the remote object accessible to remote clients, we need to create an RMI server that binds the remote object to a specific port and makes it available for remote invocation.

```java
import java.rmi.RemoteException;
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class RMIServer {
    public static void main(String[] args) {
        try {
            // Create the remote object
            SampleRemoteObject remoteObject = new SampleRemoteObject();

            // Create the RMI registry on port 1099
            Registry registry = LocateRegistry.createRegistry(1099);

            // Bind the remote object to the registry
            registry.rebind("sampleRemoteObject", remoteObject);

            System.out.println("RMI server started...");
        } catch (RemoteException e) {
            e.printStackTrace();
        }
    }
}
```

In the above example, we have created the `RMIServer` class that creates the remote object, creates an RMI registry on port 1099, and binds the remote object to the registry using a name "sampleRemoteObject".

## Step 4: Create the RMI client

Finally, we need to create a client application that will access the remote object and invoke its methods.

```java
import java.rmi.RemoteException;
import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;

public class RMIClient {
    public static void main(String[] args) {
        try {
            // Get the RMI registry on localhost, port 1099
            Registry registry = LocateRegistry.getRegistry("localhost", 1099);

            // Look up the remote object by its name
            SampleRemoteInterface remoteObject = (SampleRemoteInterface) registry.lookup("sampleRemoteObject");

            // Invoke remote methods
            remoteObject.sayHello();
            int result = remoteObject.add(3, 5);
            System.out.println("Addition result: " + result);
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

In the above example, we have created the `RMIClient` class that gets the RMI registry on localhost and port 1099, looks up the remote object by its name, and invokes its methods.

## Conclusion

Implementing remote interfaces in Java RMI allows us to build distributed applications where objects residing in different JVMs can communicate and invoke methods on each other. By following the steps outlined in this blog post, you can easily implement remote interfaces in your Java RMI applications and enable remote method invocation.

#Java #RMI