---
layout: post
title: "Asymmetric encryption in Java JCE"
description: " "
date: 2023-09-21
tags: [Java, Encryption]
comments: true
share: true
---

Asymmetric encryption is a cryptographic technique where a pair of keys is used to perform encryption and decryption of data. In Java, the Java Cryptography Extension (JCE) provides a set of classes and algorithms for implementing asymmetric encryption.

## Generating Key Pair

The first step in implementing asymmetric encryption is to generate a key pair consisting of a public key and a private key. This can be done using the `KeyPairGenerator` class in Java.

```java
import java.security.*;

public class KeyPairGeneratorExample {
    public static void main(String[] args) throws NoSuchAlgorithmException {
        // Create KeyPairGenerator instance
        KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("RSA");

        // Initialize the generator with key size
        keyPairGenerator.initialize(2048);

        // Generate the key pair
        KeyPair keyPair = keyPairGenerator.generateKeyPair();

        // Get the public key and private key
        PublicKey publicKey = keyPair.getPublic();
        PrivateKey privateKey = keyPair.getPrivate();

        // Print the keys
        System.out.println("Public Key: " + publicKey);
        System.out.println("Private Key: " + privateKey);
    }
}
```

## Encryption and Decryption

Once the key pair is generated, we can use the public key for encryption and the private key for decryption.

```java
import javax.crypto.*;
import javax.crypto.spec.SecretKeySpec;
import java.security.*;

public class AsymmetricEncryptionExample {
    public static void main(String[] args) throws NoSuchAlgorithmException, NoSuchPaddingException,
            InvalidKeyException, IllegalBlockSizeException, BadPaddingException {
        // Create KeyPairGenerator instance
        KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("RSA");
        keyPairGenerator.initialize(2048);
        KeyPair keyPair = keyPairGenerator.generateKeyPair();

        // Get the public key and private key
        PublicKey publicKey = keyPair.getPublic();
        PrivateKey privateKey = keyPair.getPrivate();

        // Plain text to be encrypted
        String plainText = "Hello, World!";

        // Create Cipher instance
        Cipher cipher = Cipher.getInstance("RSA");

        // Encryption
        cipher.init(Cipher.ENCRYPT_MODE, publicKey);
        byte[] encryptedData = cipher.doFinal(plainText.getBytes());

        // Print the encrypted data
        System.out.println("Encrypted Data: " + new String(encryptedData));

        // Decryption
        cipher.init(Cipher.DECRYPT_MODE, privateKey);
        byte[] decryptedData = cipher.doFinal(encryptedData);

        // Print the decrypted text
        System.out.println("Decrypted Text: " + new String(decryptedData));
    }
}
```

## Conclusion

Asymmetric encryption plays a vital role in securing data transmission and storage. Java JCE provides a comprehensive set of classes and algorithms to implement this encryption technique. By generating a key pair and utilizing the public and private keys, encryption and decryption can be performed easily in Java.

#Java #Encryption