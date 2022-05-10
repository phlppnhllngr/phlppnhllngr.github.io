---
title: Keys & Zertifikate
parent: Security
---

# Keys & Zertifikate

## Begriffe
- **SSL**
  - Secure Sockets Layer
  - *the standard technology for keeping an internet connection secure and safeguarding any sensitive data that is being sent between two systems* 
- **TLS**
  - Transport Layer Security
  - *an updated, more secure, version of SSL*
- **SSL Zertifikat**
  - *We still refer to our security certificates as SSL because it is a more commonly used term* 
- **RSA**
- **Zertifikat**
  - *For crypto, the certificates of interest are usually public-key certificates which bind a public-key to an identity (or sometimes a role) with some related attributes* 
  - *the most common ones by far are the public-key certificates defined by X.509*
  - *A public-key/X.509 certificate contains a publickey, but it is not merely a publickey. It contains a good deal of other information that is vital to the way it is used, although the publickey is arguably the most important single piece of information.*
  - *A certificate is created for a publickey, normally packaged as a Certificate Signing Request aka CSR or just request, by an entity called a Certificate Authority or CA which digitally signs the certificate using the CA's key so that no one else can alter it, and thus any program using it can trust it.*
  - *As a special case, it is possible to have a 'self-signed' certificate, which is signed using its own key instead of a CA's key. This certificate can't convey trust like one from a real CA, because it is NOT effectively protected against substitution, but it can be created even when you can't contact and/or pay a CA, and it can usually be processed, with manual approval or override, by programs that are designed to normally use or require a certificate.*
- **X.509**
  - *a standard created in 1988 by then-CCITT (now-ITU-T) and since enhanced and made more useful, but not fundamentally different, by many standards organizations* 
- **PKIX**
  - *The Internet standards for certificates are based on X.509 and called Public Key Infrastructure using X.509, abbreviated PKIX* 
- **CA**
  - Certificate Authority
  - *In principle anybody can act as a CA, and in particular the OpenSSL commandline program can perform the technical operations a CA does, like issuing certificates. However, in most situations the value and usefulness of a certificate depends on how well and widely the issuing CA is trusted, so the most successful CAs are the ones that have established themselves as trusted, such as Digicert-now-including-Symantec-formerly-Verisign, Comodo, GoDaddy, etc.*
- **Root Certificate** 
- **cer, crt, der, pem**
  - *CER and CRT are (both) commonly used as extensions for a file containing an X.509 certificate*
  - *There are two common encodings used for the file contents:*
    - *DER*
      - *a binary encoding (Distinguished Encoding Rules) defined by ASN.1*
    - *PEM*
      - Privacy Enhanced (e)Mail
      - *converts the binary DER to base64, broken into conveniently sized lines and with header and trailer lines added, which is more convenient for people, especially for things like cut-and-paste.*
      - *On Windows, also be careful NOT to use 'UTF-8' format which usually adds a Byte Order Mark that is not visible on the display but interferes with a program reading the file.*
      - *Although PEM is widely used for certificates and many PEM files are certificates, be aware PEM is used for many other things as well.*
- **PKCS #12, p12**
  - *defines an archive file format for storing many cryptography objects as a single file* 
  - *normally used to contain a privatekey PLUS the corresponding certificate PLUS in most cases one or more 'chain' or 'intermediate' certificate(s) that are needed to form a trust chain to validate the end-entity certificate.*
- **p12**
  - *commonly used to identify files in the PKCS12 aka PFX format*
  - *In practice PKCS12 files are always binary, although there's no technical reason they couldn't be PEM-encoded or otherwise made more human-friendly.*

### Quellen
- <https://security.stackexchange.com/a/183152>
- <https://www.websecurity.digicert.com/security-topics/what-is-ssl-tls-https>
