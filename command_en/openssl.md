openssl
===

A powerful Secure Sockets Layer (SSL) cryptography library.

## Description

**OpenSSL** is a robust, commercial-grade, and full-featured toolkit for the Transport Layer Security (TLS) and Secure Sockets Layer (SSL) protocols. It is also a general-purpose cryptography library. It includes implementations of major cryptographic algorithms, common key and certificate encapsulation management functions, and the SSL/TLS protocols. It provides a rich set of command-line tools for testing and other purposes. OpenSSL is widely used by online banking, payment systems, e-commerce sites, portals, and email services, making it one of the most critical security components on the internet.

OpenSSL has two modes of operation: interactive mode and batch mode.
Entering `openssl` without arguments starts the interactive mode, while providing commands and options runs it in batch mode.

The toolkit is primarily divided into three functional parts: the cryptography library, the SSL/TLS protocol library, and the command-line applications.

**Symmetric Cryptography Algorithms**
OpenSSL provides 8 symmetric cryptography algorithms, 7 of which are block ciphers and 1 is a stream cipher (RC4). The block ciphers include AES, DES, Blowfish, CAST, IDEA, RC2, and RC5. They support common modes such as Electronic Codebook (ECB), Cipher Block Chaining (CBC), Cipher Feedback (CFB), and Output Feedback (OFB). AES supports 128-bit block lengths for CFB and OFB, while others use 64-bit. The DES implementation includes standard DES as well as 3DES with two or three keys.

**Asymmetric Cryptography Algorithms**
OpenSSL implements 4 asymmetric cryptography algorithms: DH (Diffie-Hellman), RSA, DSA, and Elliptic Curve (EC). DH is typically used for key exchange. RSA can be used for key exchange, digital signatures, and data encryption (though it is slow for the latter). DSA is generally used only for digital signatures.

**Message Digest Algorithms**
OpenSSL implements 5 message digest algorithms: MD2, MD5, MDC2, SHA (including SHA-1), and RIPEMD. It also implements SHA-based algorithms specified in the DSS standard (DSS and DSS1).

**Key and Certificate Management**
Key and certificate management are essential parts of PKI (Public Key Infrastructure). OpenSSL provides extensive support for various standards:
- Implements ASN.1 standards for certificates and keys, supporting encoding/decoding of certificates, public/private keys, certificate requests, and CRLs in DER, PEM, and BASE64 formats.
- Provides functions and applications to generate public/private key pairs and symmetric keys.
- Supports PKCS#12 and PKCS#8 encoding/decoding for private keys.
- Implements encryption protection for private keys for secure storage and distribution.
- Supports X.509 certificate encoding/decoding, PKCS#12, and PKCS#7 formats.
- Includes a text-based database for certificate management (generation, requests, signing, revocation, and verification).
- The `ca` application acts as a simplified Certificate Authority (CA).

### Examples

**1. Generate a password using openssl**
You can use OpenSSL's random function to generate random strings for passwords.

```shell
openssl rand -base64 10
# Example output: nU9LlHO5nsuUvw==
```

**2. Message Digest examples**
Calculate the SHA1 hash of `file.txt` and output to stdout:
```shell
openssl dgst -sha1 file.txt
```

Calculate the SHA1 hash and output to `digest.txt`:
```shell
openssl sha1 -out digest.txt file.txt
```

Sign `file.txt` using DSS1 (SHA1) and output to `dsasign.bin`. The private key `dsakey.pem` must be a DSA key.
```shell
openssl dgst -dss1 -sign dsakey.pem -out dsasign.bin file.txt
```

Verify the digital signature `dsasign.bin` for `file.txt`:
```shell
openssl dgst -dss1 -prverify dsakey.pem -signature dsasign.bin file.txt
```

Sign `file.txt` using SHA1 and an RSA private key:
```shell
openssl sha1 -sign rsaprivate.pem -out rsasign.bin file.txt
```

Verify the RSA signature:
```shell
openssl sha1 -verify rsapublic.pem -signature rsasign.bin file.txt
```

**3. Symmetric Encryption examples**
Encrypt `plaintext.doc` using 3DES in CBC mode:
```shell
openssl enc -des3 -salt -in plaintext.doc -out ciphertext.bin
```

Decrypt `ciphertext.bin` using 3DES in OFB mode with a password:
```shell
openssl enc -des-ede3-ofb -d -in ciphertext.bin -out plaintext.doc -pass pass:trousers
```

Encrypt using Blowfish in CFB mode with a password from an environment variable:
```shell
openssl bf-cfb -salt -in plaintext.doc -out ciphertext.bin -pass env:PASSWORD
```

Base64 encode a file:
```shell
openssl base64 -in ciphertext.bin -out base64.txt
```

Encrypt using RC5 in CBC mode with specified salt, key, and IV:
```shell
openssl rc5 -in plaintext.doc -out ciphertext.bin -S C62CB1D49F158ADC -iv E9EDACA1BD7090C6 -K 89D4B1678D604FAA3DBFFD030A314B29
```

**4. Diffie-Hellman examples**
Generate DH parameters (1024-bit prime, generator 2):
```shell
openssl dhparam -out dhparam.pem -2 1024
```

Output DH parameters as C code:
```shell
openssl dhparam -in dhparam.pem -noout -C
```

**5. DSA examples**
Generate 1024-bit DSA parameters:
```shell
openssl dsaparam -out dsaparam.pem 1024
```

Generate a DSA private key encrypted with 3DES:
```shell
openssl gendsa -out dsaprivatekey.pem -des3 dsaparam.pem
```

Generate a public key from a private key:
```shell
openssl dsa -in dsaprivatekey.pem -pubout -out dsapublickey.pem
```

**6. RSA examples**
Generate a 1024-bit RSA private key encrypted with 3DES:
```shell
openssl genrsa -out rsaprivatekey.pem -passout pass:trousers -des3 1024
```

Extract the public key from the RSA private key:
```shell
openssl rsa -in rsaprivatekey.pem -passin pass:trousers -pubout -out rsapubckey.pem
```

Encrypt a file using the RSA public key:
```shell
openssl rsautl -encrypt -pubin -inkey rsapublickey.pem -in plain.txt -out cipher.txt
```

Decrypt a file using the RSA private key:
```shell
openssl rsautl -decrypt -inkey rsaprivatekey.pem -in cipher.txt -out plain.txt
```

**S/MIME examples**
Encrypt mail using a certificate:
```shell
openssl smime -encrypt -in mail.txt -des3 -out mail.enc cert.pem
```

Decrypt S/MIME mail:
```shell
openssl smime -decrypt -in mail.enc -recip cert.pem -inkey key.pem -out mail.txt
```

Sign mail:
```shell
openssl smime -sign -in mail.txt -signer cert.pem -inkey key.pem -out mail.sgn
```

Verify signed S/MIME mail:
```shell
openssl smime -verify -in mail.sgn -out mail.txt
```

**Other examples:**
```shell
openssl version -a
openssl help
openssl genrsa -aes128 -out fd.key 2048
openssl rsa -text -in fd.key
```
