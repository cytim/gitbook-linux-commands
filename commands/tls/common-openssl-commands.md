# SSL / TLS: Common OpenSSL Commands

> Reference: [The Most Common OpenSSL Commands](https://www.sslshopper.com/article-most-common-openssl-commands.html)


### Convert The Private Key To PKCS8 Format

```sh
openssl pkcs8 -topk8 -in server.key -nocrypt -out server.p8
```


### Extract The Key-pair From PKCS12 Keystore

**Extract the private key**

```sh
openssl pkcs12 -in server.p12 -nocerts -out server.encrypted.key
```

**Extract the certificate**

```sh
openssl pkcs12 -in server.p12 -clcerts -nokeys -out server.crt
```


### Decrypt An Encrypted Private Key

```sh
openssl rsa -in server.encrypted.key -out server.key
```

