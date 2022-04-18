# SSL/TLS CERTIFICATES (VIA OPENSSL TOOL)

## Show

Full list of standard commands
```
openssl list-standard-commands
```

Secret key algorithms available
```
openssl list-cipher-commands
```




## CSR (Certificate Signing Request)
[CSR](https://www.sslshopper.com/what-is-a-csr-certificate-signing-request.html)

> The process: Generate SSL CSR in my local computer then send the CSR to the provider and then use SSL Cert in my server. A certificate authority will use a CSR to create your SSL certificate, but it does not need your private key. You need to keep your private key secret. The certificate created with a particular CSR will only work with the private key that was generated with it. So if you lose the private key, the certificate will no longer work.

### Generate

Generate a CSR and private key
```
openssl req -out CSR.csr -new -newkey rsa:2048 -nodes -keyout privateKey.key
```

Generate a certificate signing request (CSR) for an existing private key
```
openssl req -out CSR.csr -key privateKey.key -new
```

Generate a certificate signing request based on an existing certificate
```
openssl x509 -x509toreq -in certificate.crt -out CSR.csr -signkey privateKey.key
```


### Show
What is contained in a CSR
```
openssl req -in server.csr -noout -text
```





## CERTIFICATE

### Generate
Generate a self-signed certificate
```
openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout privateKey.key -out certificate.crt

```



### Show 

What is contained in a certificate
```
openssl x509 -text -noout -in <your_cert.crt>

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

Show a public key that is contained in a certificate
```
openssl x509 -pubkey -noout -in real.crt
```

Certificate chain

```
openssl s_client -connect www.godaddy.com:443

openssl s_client -connect www.godaddy.com:443 -showcerts

```








## PUBLIC/PRIVATE KEY


### Show
What is contained in a private key
```
openssl rsa -in privateKey.key -check
```

Which public key is in the certificate
```
openssl x509 -pubkey -noout < real.crt
```


### Generate

#### Public and private key (RSA algo)

create pub and priv keys (an RSA key of 1024 bits)
```
openssl genrsa -out key.pem 1024
```
generate separate pub key for the file above
```
openssl rsa -in key.pem -pubout -out pub-key.pem
```







