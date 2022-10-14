# GPG

> GnuPG, GNU Privacy Guard, is a complete and free implementation of the OpenPGP standard as defined by [RFC4880](https://www.ietf.org/rfc/rfc4880.txt) (also known as PGP). GnuPG allows you to encrypt and sign your data and communications.
>
> \- [gnupg.org](https://gnupg.org/)

## Cheat Sheet

- [Generating a new GPG key](https://docs.github.com/en/authentication/managing-commit-signature-verification/generating-a-new-gpg-key)
- [How to use GPG to encrypt stuff](https://yanhan.github.io/posts/2017-09-27-how-to-use-gpg-to-encrypt-stuff/)

## Keys Management

### Generate A New Key

```sh
# You will be prompted with a few questions. Follow the instructions to generate the key.
gpg --full-generate-key
```

### List Keys

```sh
# List the private keys
gpg --list-secret-keys [--keyid-format=long]

# List the public keys
gpg --list-keys [--keyid-format=long]
```

### Export Keys

```sh
# Export the private key
gpg --output /path/to/output/private.asc --armor --export-secret-key KEY_ID

# Export the public key
gpg --output /path/to/output/public.asc --armor --export KEY_ID
```

### Import Key

```sh
gpg --import /path/to/key
```

### Delete Keys

```sh
# Delete private keys
gpg --delete-secret-key KEY_ID [...KEY_IDS]

# Delete public keys
# - If the public key is associated with the private key, the private key has to be deleted first.
gpg --delete-key KEY_ID [...KEY_IDS]
```

## Encryption/Decryption

```sh
# Encrypt the file
# - You must first import the public key of the recipient.
gpg --output /path/to/encrypted.txt.gpg --encrypt --recipient someone@example.com /path/to/plain.txt

# Decrypt the file
# - You will need the corresponding private key.
gpg --output /path/to/plain.txt --decrypt /path/to/encrypted.txt.gpg
```

## Signature

```sh
# Sign the message
shasum -a 256 /path/to/file.txt | awk '{print $1}' > /path/to/file.txt.sha256sum
gpg --output /path/to/file.txt.sha256sum.sig --sign /path/to/file.txt.sha256sum

# Verify the signature
gpg --verify /path/to/file.txt.sha256sum.sig
```
