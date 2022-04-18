## Overall

When someone refers to an `RSA` certificate, what they're talking about is an `SSL` certificate that uses the `RSA` algorithm for digital signatures and/or data encryption. 

`RSA (Rivest–Shamir–Adleman)` is a cryptographic algorithm that encrypts and decrypts the data.

RSA key is a private key based on RSA algorithm. Private Key is used for authentication and a symmetric key exchange during establishment of an SSL/TLS session. It is a part of the public key infrastructure that is generally used in case of SSL certificates.


In asymmetric encryption (also known as “public-key cryptography”), one key encrypts the data while the other key is used to decrypt it. 

For example, in SSL/TLS enabled websites, the public key encrypts the data while the private key, which is stored securely on the webserver, decrypts the data. This way, we can achieve three things:
- Authentication – Only the intended recipient will be able to see your data.
- Encryption – As the data is encrypted and cannot be decrypted without the private key, no one can come in between and steal or tamper with the data.
- Integrity - The recipient of the data/message can be sure that it has remained in the form the sender sent it.
    
## Generate 

Private Key
```
openssl genrsa -out xbs.key 1024
```

Public Key
```
openssl rsa -in xbs.key -pubout > xbs.pem
```




































