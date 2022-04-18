# SSL/TLS CERTIFICATES

## Overall

When someone refers to an `RSA certificate`, what they’re talking about is an `SSL certificate` that uses the `RSA algorithm` for digital signatures and/or data encryption.

`RSA` (Rivest–Shamir–Adleman) is a cryptographic algorithm that encrypts and decrypts the data. Invented in the year 1978, RSA was named after Rivest, Shamir, and Adleman – the mathematicians who invented it.

The fundamental function of an `RSA certificate` is to use the `RSA algorithm` for data encryption.

The `RSA certificate` uses an encryption algorithm that encrypts data so that unauthorized parties cannot see it or tamper with it. 

The encryption process is done by what’s known as “encryption keys.” 

Depending upon the function of encryption keys, encryption can be classified into two types:
- symmetric encryption
- asymmetric encryption.

`Symmetric encryption` involves one key that is utilized to encrypt as well as decrypt the data. It’s kind of like a password. 

`Asymmetric encryption`, on the other hand, is quite the opposite to the method that is symmetric encryption. 

It involves two cryptographic keys, regarded as `public key` and `private key`. 

Both these keys are distinct but are mathematically related to each other. 

The `public key`, as you can understand by its name, is publicly available. The `private key` is supposed to be kept secret. That’s why some even refer to it as ‘secret key.’


`RSA key` is a `private key` based on `RSA algorithm`.

It is a part of the public key infrastructure that is generally used in case of `SSL certificates`. 

A public key infrastructure assumes asymmetric encryption where two types of keys are used:
- Private Key
- Public Key (it is included in an `SSL certificate`). 

Since encrypted data transmission takes too much time in case of asymmetric encryption, this kind of encryption is used for a secure symmetric key exchange that is used for actual transmitted data encryption and decryption. 






## Show `openssl` options

Full list of standard commands
```
openssl list-standard-commands
```

Secret key algorithms available
```
openssl list-cipher-commands
```



## CSR (Certificate Signing Request)

You can order a certificate via [CSR](https://www.sslshopper.com/what-is-a-csr-certificate-signing-request.html).

The ordering process: 
- generate simultaneosuly:
   - private key
   - SSL `Certificate Signing Request (CSR)` on the local computer, which contains:
       - Country Name;
       - Organization Name;
       - Email Address;
       - etc
- send only generated `CSR` to the provider (`private key` is left you your side secretly);
- provider will send a `SSL Certificate` back to you;
- use `SSL Certificate` in the necessary server.

A `Certificate Authority` will use a `CSR` to create your `SSL certificate`, but it does not need your `private key`. 

You need to keep your `private key` secret. 

The certificate created with a particular `CSR` will only work with the `private key` that was generated with it. 

> **NOTE**: So if you lose the `private key`, the `certificate` will no longer work.


### Show CSR content

What is contained in a CSR
```
openssl req -in CSR.csr -noout -text
```


### Generate CSR

> **NOTE**: Usually, an `RSA Private Key` is generated in pair with a `CSR`.

> **NOTE**: During `CSR`/`Private Key` generation, as a rule, it is possible to specify the key size. 
> Nowadays most of the Certificate Authorities consider `2048`-bit as an optimal key size for a `RSA Private Key`, since it provides a decent level of security and does not load the server’s CPU much. 
> If you wish, you can use a `4096`-bit key size for your `Private Key` with our certificates as well, however every doubling of an `RSA Private Key` slows down an `SSL/TLS handshake` approximately by 6-7 times. 


Generate new `CSR` and new `private key`
```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privateKey.key
```

Generate new `CSR`, based on old `private key` (the one that already exists)
```
openssl req -out CSR.csr -key privateKey.key -new
```

Generate new `CSR`, based on both old (already existing):
- `certificate`
- `private key` 
```
openssl x509 -x509toreq -in certificate.crt -out CSR.csr -signkey privateKey.key
```




## Certificate

### Generate

Generate a self-signed `certificate` and corresponding `private key`
```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt
```


### Show 

What is contained in a certificate
```
openssl x509 -text -noout -in certificate.crt

Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            ...
    Signature Algorithm: sha256WithRSAEncryption
        Issuer: C=GB, ST=Greater Manchester, L=Salford, O=Sectigo Limited, CN=Sectigo RSA Domain Validation Secure Server CA
        Validity
            Not Before: Nov 17 00:00:00 2021 GMT
            Not After : Nov 30 23:59:59 2022 GMT
        Subject: CN=*.<your_domain>
        ...
```

Show a `public key` that is contained in a certificate
```
openssl x509 -pubkey -noout -in certificate.crt
```

Show certificate chain

```
openssl s_client -connect www.godaddy.com:443

openssl s_client -connect www.godaddy.com:443 -showcerts
```





## Public/Private Keys


### Show keys

What is contained in a `private key`
```
openssl rsa -in privateKey.key -check
```

Which `public key` is in the `certificate`
```
openssl x509 -pubkey -noout < real.crt

  # OR
  
openssl x509 -pubkey -noout -in certificate.crt
```


### Generate keys

> **NOTE**: Usually, an `RSA Private Key` is generated in pair with a `CSR`.
> See appropriate block above.

> **NOTE**: During `CSR`/`Private Key` generation, as a rule, it is possible to specify the key size. 
> Nowadays most of the Certificate Authorities consider `2048`-bit as an optimal key size for a `RSA Private Key`, since it provides a decent level of security and does not load the server’s CPU much. 
> If you wish, you can use a `4096`-bit key size for your `Private Key` with our certificates as well, however every doubling of an `RSA Private Key` slows down an `SSL/TLS handshake` approximately by 6-7 times. 


Generate new `private key`
```
openssl genrsa -out privateKey.pem 1024
```

Generate new `public key` for already existing `private key`
```
openssl rsa -in privateKey.pem -pubout -out publicKey.pem
```






















