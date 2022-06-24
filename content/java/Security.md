---
title: Security
parent: Java
---

# Security

## Keystore
- *Keystore in Java can refer to three things, depending on the context. (They're all closely related but subtly different.)*
- *can be a repository where private keys, certificates and symmetric keys can be stored. This is typically a file, but the storage can also be handled in different ways (e.g. cryptographic token or using the OS's own mechanism.)*
- *also a class which is part of the standard API. It is essentially a way to load, save and generally interact with one of the "physical" keystores as described above. A KeyStore can also be purely in memory, if you just need the API abstraction for your application.*
- *can also be used as the counterpart of "truststore". This is where it can get confusing, since both "keystore" and "truststore" are keystores, they're just used for different purposes.*
  - **keystore**
    - *is used to initialise the key manager. A KeyManager determines which authentication credentials to send to the remote host.*
    - *will contain your own certificate and its private key: this is what you're going to use to authenticate yourself to a remote party (when required).*
  - **truststore**
    - *is used to initialise the trust manager. A TrustManager determines whether the remote authentication credentials (and thus the connection) should be trusted.*
    - *will contain a number of (CA) certificates that you're willing to trust*
    - *There is a default truststore bundled with the JRE (/lib/security/cacerts). There isn't a default keystore, since it's usually a more explicit step for the user. This repository can be modified with the keytool command that ships with the JRE.*
    - *For each release, the Java team will review world-wide top level root CA (Certificate Authority) certificates at the release. All valid root CA certificates will be included in default trusted certificate keystore file: "cacerts". For Java 15 released in 2020, the default trusted certificate keystore file, "cacerts", includes 92 trusted certificates*
    - *TrustManagerFactory uses the following steps to try to find trust material: system property `javax.net.ssl.trustStore`, java-home/lib/security/jssecacerts, java-home/lib/security/cacerts (shipped by default). If there is a jssecacerts file it is used exclusively - not in addition to the cacerts file. My recommendation: keep the cacerts file, copy to jssecacerts and add any private CA/Signing certs needed to the jssecacerts file.*
    - *Typically, the error you're getting ("ValidatorException: PKIX path building failed") happens when the certificate of the server you're connecting to cannot be verified using any certificate in the truststore you're using.*


## JCA/JCE API
- Java Cryptography Architecture, Java Cryptography Extension
  - Interfaces & Klassen
    - Security
    - KeyGenerator -> generates symmetric keys
    - Key
    - Cipher -> Encryption algorithm
    - KeyPair -> public/private key pair
    - KeyStore -> Storing mechanism for keys and certificates
    - MessageDigest -> hashing
    - Signature
    - Certificate
    - ...
    - <https://docs.oracle.com/javase/8/docs/api/java/security/package-summary.html>
- Providers/Impls: SunJCE (JDK), BouncyCastle (3rd Party), ...
- Einen Security-Provider registrieren
  - programmatisch
    - `java.security.Security.addProvider(java.security.Provider impl)`
  - per java.security-File
    ```
    security.provider.1=sun.security.provider.Sun
    security.provider.2=com.someprovider.SomeProvider
    ```
    - Java 8: jre/lib/security/java.security, 3rd Party Jars nach lib/ext
    - Java 9+: conf/security/java.security, 3rd Party Jars im Classpath
- **Hashing**
  - Pseudo-random, one-way
  - MessageDigest
    - `static MessageDigest getInstance("SHA-256")`
    - `byte[] digest(byte[] input)`
- **Symmetric Encryption**
  - KeyGenerator
    - `static KeyGenerator getInstance("AES")`
    - `Key generateKey`
  - Cipher
    - `static Cipher getInstance("AES/ECB/PKCS5Padding")`
    - `void init(Cipher.ENCRYPT_MODE, Key)`
    - `byte[] doFinal(byte[] input)`
- **Asymmetric Encryption**
  - ensures confidentiality
  - KeyPairGenerator
    - `KeyPair generateKeyPair`
  - Cipher
    - `static Cipher getInstance("RSA")`
    - `void init(Cipher.ENCRYPT_MODE, keyPair.getPrivate())`
    - `void init(Cipher.DECRYPT_MODE, keyPair.getPublic())`
  - Digital signatures
    - ensures integrity
    - Signature
      - `static Signature getInstance("SHA256WithRSA")`
      - `void initSign(keyPair.getPrivate())`
      - `void update(byte[] input)`
      - `byte[] sign()`
      - `void initVerify(keyPair.getPublic())`
      - `boolean verify(byte[] signed)`
      - <https://docs.oracle.com/javase/8/docs/api/java/security/Signature.html>
  - Certificates
    - ensures authenticity
    - KeyStore
      - `KeyStore static getInstance("JKS")`
      - `load(inputStream, keystorePassword)` (.jks, .jceks, .pkcs12)
      - `Key getKey(alias, keyPassword)`
      - `Certificate getCertificate(alias)`
- [Cryptography 101 for Java developers by Michel Schudel](https://www.youtube.com/watch?v=1925zmDP_BY)

