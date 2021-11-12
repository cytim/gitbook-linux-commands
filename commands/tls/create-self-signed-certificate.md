# SSL / TLS: Create A Self-signed Certificate

### Without Root CA

```sh
openssl req -new -newkey rsa:2048 -days 365 -nodes -x509 -keyout server.key -out server.crt
```

### With Root CA

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

