---
layout: post
title: "Encrypting and decrypting data using Java Cipher wrapper class"
description: " "
date: 2023-09-14
tags: [Tech,Encryption, DataSecurity]
comments: true
share: true
---

Data encryption plays a crucial role in protecting sensitive information, both at rest and in transit. In Java, the `Cipher` class is used for cryptographic encryption and decryption operations. This blog post will guide you through the process of encrypting and decrypting data using the `Cipher` wrapper class in Java.

## Encryption

Encryption is the process of converting plain text into an unreadable format called ciphertext. Let's see an example of encrypting data using the `Cipher` class in Java:

```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;

public class DataEncryption {

    public static void main(String[] args) throws Exception {
        // Generate a secret key
        KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
        keyGenerator.init(128);
        SecretKey secretKey = keyGenerator.generateKey();

        // Create a Cipher object
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.ENCRYPT_MODE, secretKey);

        // Encrypt the data
        byte[] input = "Sensitive data".getBytes();
        byte[] encryptedData = cipher.doFinal(input);

        System.out.println("Encrypted Data: " + new String(encryptedData));
    }
}
```

In the above example, we first generate a secret key using the `KeyGenerator` class. We then create a `Cipher` object using the "AES" algorithm. Next, we initialize the cipher in encryption mode by passing the secret key and specifying `Cipher.ENCRYPT_MODE`. Finally, we encrypt the data by calling `cipher.doFinal(input)`.

## Decryption

Decryption is the process of converting ciphertext back into plain text. Here's an example of decrypting data using the `Cipher` class in Java:

```java
import javax.crypto.Cipher;
import javax.crypto.SecretKey;

public class DataDecryption {

    public static void main(String[] args) throws Exception {
        // Same secret key should be used for decryption
        SecretKey secretKey = ...; // Retrieve or generate the secret key

        // Create a Cipher object
        Cipher cipher = Cipher.getInstance("AES");
        cipher.init(Cipher.DECRYPT_MODE, secretKey);

        // Decrypt the data
        byte[] encryptedData = ...; // Retrieve the encrypted data
        byte[] decryptedData = cipher.doFinal(encryptedData);
        
        System.out.println("Decrypted Data: " + new String(decryptedData));
    }
}
```

In the above example, we assume that you have a valid `SecretKey` object for decryption. We create a `Cipher` object similar to the encryption process, but this time we pass `Cipher.DECRYPT_MODE` to initialize the cipher for decryption. Finally, we decrypt the data by calling `cipher.doFinal(encryptedData)`.

## Conclusion

In this blog post, we explained how to use the `Cipher` class to encrypt and decrypt data in Java. It is important to store and manage the secret key securely to ensure the confidentiality of the encrypted data. Keep in mind that encryption alone is not sufficient for data security, but it is an important component in protecting sensitive information.

#Tech #Java #Encryption #DataSecurity