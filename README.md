# Crypto Toolkit

A browser-based cryptography toolkit built with plain JavaScript and the Web Crypto API. No libraries, no installs, no server.

**Live demo:** https://fevenadane586-design.github.io/crypto-toolkit/

## Features

- **Encrypt / Decrypt:** AES-256-GCM authenticated encryption with a password
- **Hashing:** SHA-1, SHA-256 and SHA-512 of any text
- **File integrity:** SHA-256 of any file, with a compare box to verify downloads
- **Breach check:** tests a password against the Have I Been Pwned database using k-anonymity

## How it works

**Encryption.** The password is turned into a 256-bit key using PBKDF2-SHA-256 with 600,000 iterations and a random 16-byte salt. The text is encrypted with AES-GCM using a random 12-byte IV. The output is the salt, IV and ciphertext combined and encoded in Base64. GCM also authenticates the data, so a wrong password or any tampering makes decryption fail.

**Breach check.** The browser computes the SHA-1 hash of the password and sends only the first 5 hex characters to the API. The API returns all matching hash suffixes, and the comparison happens locally. The full password and full hash never leave the browser.

**File integrity.** Comparing a file's hash with the publisher's hash shows whether the file was corrupted or modified.

## What I learned

- The difference between hashing, encryption and key derivation
- Why salts and IVs must be random and unique
- Why slow key derivation (PBKDF2) makes password guessing harder
- How k-anonymity lets a service answer a query without learning the secret

## Limitations

- Educational project, not security audited. Do not use it for real secrets.
- SHA-1 is included for the breach API and comparison only, and is not safe for security purposes.
- Encrypted data cannot be recovered if the password is lost.

## Future improvements

- Encrypt and decrypt files
- Password generator
- Add HMAC support

## License

MIT
