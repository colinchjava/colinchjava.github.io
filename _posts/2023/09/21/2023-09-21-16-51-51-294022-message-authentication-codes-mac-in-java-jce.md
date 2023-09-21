---
layout: post
title: "Message authentication codes (MAC) in Java JCE"
description: " "
date: 2023-09-21
tags: [java]
comments: true
share: true
---

Message Authentication Codes (MAC) are cryptographic algorithms that are used to verify the integrity and authenticity of a message. They use a secret key to create a fixed-size digest of the message, allowing the receiver to verify the integrity of the message and detect any modifications.

In Java, the Java Cryptography Extension (JCE) provides a set of classes and APIs to perform various cryptographic operations, including generating and verifying MACs. In this blog post, we will explore how to generate and verify MACs using Java JCE.

## Generating a MAC

To generate a MAC using Java JCE, you need to follow these steps:

1. Choose an appropriate MAC algorithm: Java JCE supports various MAC algorithms, such as HMAC (Hash-based MAC) and CMAC (Cipher-based MAC). You can choose the algorithm based on your requirements, like HMAC-SHA256 or CMAC-AES.

2. Create a `SecretKeySpec` object: The `SecretKeySpec` class is used to construct a secret key from a byte array. You need to provide the byte array representation of your secret key and the MAC algorithm name.

3. Initialize a `Mac` object: The `Mac` class is used to perform the actual MAC computation. You need to create an instance of the `Mac` class, initialize it with the chosen algorithm, and set the secret key using the `init()` method.

4. Update the `Mac` object with the message data: You can update the `Mac` object with the message data using the `update()` method. You can do this in one go if you have the entire message in memory, or update the `Mac` object multiple times if the message is large or streamed.

5. Generate the MAC: Finally, you can generate the MAC by calling the `doFinal()` method on the `Mac` object. This will return the computed MAC value as a byte array.

Here's an example code snippet that demonstrates how to generate a MAC using Java JCE:

```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.security.Key;
import java.security.NoSuchAlgorithmException;
import java.security.InvalidKeyException;

public class MacGenerator {

    public static byte[] generateMac(byte[] message, byte[] secretKey, String algorithm) throws NoSuchAlgorithmException, InvalidKeyException {
        Key secretKeySpec = new SecretKeySpec(secretKey, algorithm);
        Mac mac = Mac.getInstance(algorithm);
        mac.init(secretKeySpec);
        mac.update(message);
        return mac.doFinal();
    }

    public static void main(String[] args) {
        String message = "Hello, world!";
        String secretKey = "secretpassword";
        String algorithm = "HmacSHA256";

        try {
            byte[] mac = generateMac(message.getBytes(), secretKey.getBytes(), algorithm);
            System.out.println("Generated MAC: " + bytesToHex(mac));
        } catch (NoSuchAlgorithmException | InvalidKeyException e) {
            e.printStackTrace();
        }
    }

    private static String bytesToHex(byte[] bytes) {
        StringBuilder result = new StringBuilder();
        for (byte b : bytes) {
            result.append(String.format("%02x", b));
        }
        return result.toString();
    }
}
```

In the above code, we generate a HMAC-SHA256 MAC for the message "Hello, world!" using the secret key "secretpassword". The generated MAC is then printed to the console.

## Verifying a MAC

To verify a MAC using Java JCE, you need to follow these steps:

1. Obtain the MAC value to verify: This could be obtained from the message source or sent along with the message.

2. Create a `SecretKeySpec` object: Similar to MAC generation, you need to create a `SecretKeySpec` object using the same secret key and MAC algorithm.

3. Initialize a `Mac` object: Initialize a `Mac` object with the MAC algorithm and the secret key using the `init()` method.

4. Update the `Mac` object with the message data: Update the `Mac` object with the same message data that was used to generate the MAC.

5. Verify the MAC: To verify the MAC, you can compare the computed MAC value (using the `doFinal()` method) with the obtained MAC value. If they match, the message integrity is verified.

Here's an example code snippet that demonstrates how to verify a MAC using Java JCE:

```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;
import java.security.Key;
import java.security.NoSuchAlgorithmException;
import java.security.InvalidKeyException;

public class MacVerifier {

    public static boolean verifyMac(byte[] message, byte[] secretKey, byte[] receivedMac, String algorithm) throws NoSuchAlgorithmException, InvalidKeyException {
        Key secretKeySpec = new SecretKeySpec(secretKey, algorithm);
        Mac mac = Mac.getInstance(algorithm);
        mac.init(secretKeySpec);
        byte[] computedMac = mac.doFinal(message);
        return MessageDigest.isEqual(receivedMac, computedMac);
    }

    public static void main(String[] args) {
        String message = "Hello, world!";
        String secretKey = "secretpassword";
        String algorithm = "HmacSHA256";
        byte[] receivedMac = hexToBytes("d5bfb5e0aef430da2419e1f2d227f488f8867eab2833d16d4db5a80c411db12c");

        try {
            boolean isMacValid = verifyMac(message.getBytes(), secretKey.getBytes(), receivedMac, algorithm);
            if (isMacValid) {
                System.out.println("MAC verification passed.");
            } else {
                System.out.println("MAC verification failed!");
            }
        } catch (NoSuchAlgorithmException | InvalidKeyException e) {
            e.printStackTrace();
        }
    }

    private static byte[] hexToBytes(String hex) {
        int len = hex.length();
        byte[] data = new byte[len / 2];
        for (int i = 0; i < len; i += 2) {
            data[i / 2] = (byte) ((Character.digit(hex.charAt(i), 16) << 4)
                    + Character.digit(hex.charAt(i+1), 16));
        }
        return data;
    }
}
```

In the above code, we verify the MAC value received ("d5bfb5e0aef430da2419e1f2d227f488f8867eab2833d16d4db5a80c411db12c") for the message "Hello, world!" using the secret key "secretpassword" and the HMAC-SHA256 algorithm. The verification result is then printed to the console.

#java #JCE