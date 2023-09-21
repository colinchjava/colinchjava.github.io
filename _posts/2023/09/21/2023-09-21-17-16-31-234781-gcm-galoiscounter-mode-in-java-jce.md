---
layout: post
title: "GCM (Galois/Counter Mode) in Java JCE"
description: " "
date: 2023-09-21
tags: [Java]
comments: true
share: true
---

GCM (Galois/Counter Mode) is an authenticated encryption mode that provides both confidentiality and integrity of data. In Java, the Java Cryptography Extension (JCE) provides support for GCM through the `Cipher` class. In this blog post, we will explore how to use GCM in Java JCE to encrypt and decrypt data.

### Setting Up the Encryption

To use GCM in Java JCE, we first need to set up the encryption process. This involves initializing the cipher, generating a key, and setting the parameters for the GCM mode.

```java
import javax.crypto.Cipher;
import javax.crypto.KeyGenerator;
import javax.crypto.SecretKey;
import javax.crypto.spec.GCMParameterSpec;
import java.security.NoSuchAlgorithmException;
import java.security.SecureRandom;

public class GCMExample {
    private static final int GCM_TAG_LENGTH = 128;
    private static final int GCM_NONCE_LENGTH = 12;

    public static void main(String[] args) throws Exception {
        // Generate a random 128-bit AES key
        KeyGenerator keyGenerator = KeyGenerator.getInstance("AES");
        keyGenerator.init(128);
        SecretKey secretKey = keyGenerator.generateKey();

        // Generate a random nonce
        SecureRandom secureRandom = new SecureRandom();
        byte[] nonce = new byte[GCM_NONCE_LENGTH];
        secureRandom.nextBytes(nonce);

        // Create the GCM parameter spec
        GCMParameterSpec gcmParameterSpec = new GCMParameterSpec(GCM_TAG_LENGTH, nonce);

        // Initialize the cipher
        Cipher cipher = Cipher.getInstance("AES/GCM/NoPadding");
        cipher.init(Cipher.ENCRYPT_MODE, secretKey, gcmParameterSpec);

        // Perform the encryption
        byte[] plaintext = "Hello, GCM!".getBytes();
        byte[] ciphertext = cipher.doFinal(plaintext);

        System.out.println("Ciphertext: " + new String(ciphertext));
    }
}
```

In this example, we first generate a random 128-bit AES key using `KeyGenerator`. We then generate a random nonce using `SecureRandom`. The GCM parameter spec is created using the tag length and the nonce. Finally, we initialize the cipher with the secret key and the GCM parameter spec.

### Decrypting the Data

Once the data is encrypted, we can decrypt it using the same key and GCM parameters. Here's how to decrypt the ciphertext:

```java
// ...

// Initialize the cipher for decryption
cipher.init(Cipher.DECRYPT_MODE, secretKey, gcmParameterSpec);

// Perform the decryption
byte[] decryptedText = cipher.doFinal(ciphertext);

System.out.println("Decrypted Text: " + new String(decryptedText));
```

In the decryption process, we initialize the cipher with the secret key and the same GCM parameter spec used for encryption. We then call `doFinal` to decrypt the ciphertext.

### Conclusion

GCM provides a secure and efficient way to encrypt and authenticate data. In Java, the JCE allows us to easily use GCM through the `Cipher` class. By setting up the cipher and using the appropriate parameters, we can achieve confidentiality and integrity in our data encryption.

If you are interested in GCM and encryption in general, make sure to explore and experiment with the other available algorithms and modes offered by the Java Cryptography Extension.

\#GCM #Java