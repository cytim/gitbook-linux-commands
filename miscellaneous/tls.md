# SSL / TLS


### Create A Self-signed Certificate

1. Create a root CA.

    ```sh
    # generate the private key
    openssl genrsa -out ca.key 2048 -nodes
    # generate the certificate
    openssl req -new -x509 -key ca.key -out ca.crt -days 3650
    ```

    > `-days`: number of days the certificate will be valid for.

2. Create a server private key and Certificate Signing Request (CSR).

    ```sh
    # generate the private key
    openssl genrsa -out server.key 2048
    # generate the CSR to be signed
    openssl req -new -key server.key -out server.csr
    ```

3. Sign the CSR by the root CA.

    ```sh
    openssl x509 -req -days 365 -in server.csr -CA ca.crt -CAkey ca.key -CAcreateserial -out server.crt
    ```

    > `-days`: number of days the certificate will be valid for.


### Convert The Private Key To PKCS8 Format

```sh
openssl pkcs8 -topk8 -in server.key -nocrypt -out server.p8
```


### Import The Key-pair Into Java Keystore

1. Convert the key-pair into PKCS12 keystore.

    ```sh
    openssl pkcs12 -export -in server.crt -inkey server.key -out server.p12 -passout env:KEYPAIR_PWD -name server-name
    ```

    > `-passout`: `env:<VAR_NAME>` / `file:<PATH>` / `fd:<NUM>` / `stdin`

2. Import the PKCS12 keystore into the Java keystore.

    ```sh
    keytool -importkeystore -noprompt -srckeystore server.p12 -srcstoretype pkcs12 -srcstorepass <KEYPAIR_PWD> -destkeystore server.jks -deststoretype JKS -deststorepass <KEYSTORE_PWD>
    ```

    > Reference: https://www.ssl.com/how-to/create-a-pfx-p12-certificate-file-using-openssl/

3. Check-out [here](https://www.sslshopper.com/article-most-common-java-keytool-keystore-commands.html) for the list of the most common Java keytool commands.


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

