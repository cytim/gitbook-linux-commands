# SSL / TLS: Java Truststore and Keystore


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

