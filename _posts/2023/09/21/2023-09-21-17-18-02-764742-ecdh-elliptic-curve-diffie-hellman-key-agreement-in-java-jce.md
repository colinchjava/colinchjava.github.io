---
layout: post
title: "ECDH (Elliptic Curve Diffie-Hellman) key agreement in Java JCE"
description: " "
date: 2023-09-21
tags: [tech, security]
comments: true
share: true
---

In this blog post, we will walk through how to perform Elliptic Curve Diffie-Hellman (ECDH) key agreement in Java using the Java Cryptography Extension (JCE) library. ECDH is a key exchange algorithm that allows two parties to establish a shared secret over an insecure channel. The shared secret can then be used as a symmetric key for encryption or other secure purposes.

## Prerequisites
To follow along, make sure you have Java Development Kit (JDK) installed on your system. Additionally, you may need to install the Java Cryptography Extension Unlimited Strength Jurisdiction Policy Files for your specific JDK version.

## Generating a Key Pair
First, we need to generate a key pair for both the server and the client. We will be using the **secp256r1** elliptic curve for our example.

```java
import java.security.*;

public class KeyGenerator {

   public static KeyPair generateKeyPair() throws NoSuchAlgorithmException {
       KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("EC");
       ECGenParameterSpec parameterSpec = new ECGenParameterSpec("secp256r1");
       keyPairGenerator.initialize(parameterSpec);
       return keyPairGenerator.generateKeyPair();
   }

   public static void main(String[] args) throws Exception {
       KeyPair keyPair = generateKeyPair();
       PrivateKey privateKey = keyPair.getPrivate();
       PublicKey publicKey = keyPair.getPublic();

       System.out.println("Private Key: " + privateKey);
       System.out.println("Public Key: " + publicKey);
   }
}
```

## Performing Key Agreement
Now that we have generated the key pair for both the server and the client, we can perform the key agreement.

```java
import javax.crypto.KeyAgreement;
import java.security.*;

public class KeyAgreementExample {
   
   public static void main(String[] args) throws Exception {
       KeyPairGenerator keyPairGenerator = KeyPairGenerator.getInstance("EC");
       ECGenParameterSpec parameterSpec = new ECGenParameterSpec("secp256r1");
       keyPairGenerator.initialize(parameterSpec);

       // Generate server's key pair
       KeyPair serverKeyPair = keyPairGenerator.generateKeyPair();
       PrivateKey serverPrivateKey = serverKeyPair.getPrivate();
       PublicKey serverPublicKey = serverKeyPair.getPublic();

       // Generate client's key pair
       KeyPair clientKeyPair = keyPairGenerator.generateKeyPair();
       PrivateKey clientPrivateKey = clientKeyPair.getPrivate();
       PublicKey clientPublicKey = clientKeyPair.getPublic();

       // Perform the key agreement
       KeyAgreement keyAgreement = KeyAgreement.getInstance("ECDH");
       keyAgreement.init(serverPrivateKey);
       keyAgreement.doPhase(clientPublicKey, true);
       SecretKey sharedSecret = keyAgreement.generateSecret();

       // Print the shared secret
       byte[] sharedSecretBytes = sharedSecret.getEncoded();
       System.out.println("Shared Secret: " + Hex.encodeHexString(sharedSecretBytes));
   }
}
```

## Conclusion
In this blog post, we explored how to perform ECDH key agreement in Java using the JCE library. This key exchange algorithm allows two parties to establish a shared secret over an insecure channel. We generated key pairs for the server and client, and then performed the key agreement. The resulting shared secret can be used for encryption or other secure purposes.

#tech #security