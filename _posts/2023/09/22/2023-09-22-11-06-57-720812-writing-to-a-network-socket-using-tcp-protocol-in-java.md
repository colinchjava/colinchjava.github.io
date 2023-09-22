---
layout: post
title: "Writing to a network socket using TCP protocol in Java"
description: " "
date: 2023-09-22
tags: [TCPProtocol, JavaNetworkCommunication]
comments: true
share: true
---

In Java, you can establish a TCP connection and write data to a network socket using the `Socket` and `OutputStream` classes. This is commonly done when implementing network communication applications, such as client-server systems or network protocols.

Below is an example code that demonstrates how to write to a network socket using the TCP protocol in Java:

```java
import java.io.*;
import java.net.*;

public class TCPClient {

    public static void main(String[] args) {
        String serverHostname = "example.com";
        int serverPort = 1234;

        try {
            // Connect to the server
            Socket socket = new Socket(serverHostname, serverPort);

            // Get the output stream
            OutputStream outputStream = socket.getOutputStream();

            // Create a writer to write data to the stream
            PrintWriter writer = new PrintWriter(outputStream, true);

            // Write data to the socket
            String message = "Hello, server!";
            writer.println(message);

            // Close the writer and socket
            writer.close();
            socket.close();
        } catch (UnknownHostException e) {
            System.err.println("Error: Unknown host " + serverHostname);
        } catch (IOException e) {
            System.err.println("Error: I/O exception occurred");
        }
    }
}
```

In the code above, we first specify the server hostname and port number that we want to connect to. Then, we create a `Socket` object by providing the server's hostname and port. We obtain the output stream from the socket using the `getOutputStream()` method. 

To write data to the socket, we create a `PrintWriter` object and pass the output stream to its constructor. The `println()` method is then used to write the data to the socket. Finally, we close the writer and socket to release resources.

Remember to replace `example.com` with the actual hostname of the server you want to connect to, and `1234` with the appropriate port number.

By following the above example, you can easily write data to a network socket using TCP protocol in Java. This can be utilized in various network communication scenarios, enabling seamless data exchange between client and server systems.

**#TCPProtocol #JavaNetworkCommunication**