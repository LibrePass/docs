# Security

## What does the server store?

The server only stores data that is encrypted on the local device before sending it.
So your secrets are safe and always yours!

## KDF Algorithm (Key Derivation Function)

LibrePass first derives a key from your master password using the [Argon2](#argon2id) algorithm.
This key is then used to decrypt the encryption key which is retrieved from the server in encrypted form.
Before sending the key to the server, it has additional iterations using [PBKDF2-SHA256](#pbkdf2-sha256)
because the earlier key was used for encryption key encryption.

### Argon2id

LibrePass uses the Argon2id variant of [Argon2](https://en.wikipedia.org/wiki/Argon2). 
This variant is resistant to side-channel attacks and GPU cracking.

#### Default Parameters (client-side)

Client-side parameters are used to derive the key for encryption key encryption.
They are not sent to the server. Sent to the server is the key after additional [PBKDF2-SHA256](#pbkdf2-sha256) iterations.

| Parameter   | Value        |
|-------------|--------------|
| Memory      | 64 MB        |
| Iterations  | 4            |
| Parallelism | 3            |
| Salt        | (user email) |
| Hash Length | 32 bytes     |

#### Server Parameters (server-side)

Server-side parameters are used to compute a hash that is stored in the database.

| Parameter   | Value    |
|-------------|----------|
| Memory      | 15 MB    |
| Iterations  | 1        |
| Parallelism | 1        |
| Salt        | 32 bytes |
| Hash Length | 32 bytes |

### PBKDF2-SHA256

[PBKDF2-SHA256](https://en.wikipedia.org/wiki/PBKDF2) is used to derive the final password hash, which is sent to the server to authenticate the user.
It is computed from the hash after [Argon2id](#argon2id) iterations.

| Parameter   | Value           |
|-------------|-----------------|
| Iterations  | 1               |
| Salt        | (user password) |
| Hash Length | 32 bytes        |

## Encryption

### AES-CBC

[AES](https://en.wikipedia.org/wiki/Advanced_Encryption_Standard)-CBC 
([Cipher Block Chaining](https://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher_block_chaining_(CBC)))
is used to encrypt secrets. The key for encryption/decryption is encryption key, 
which is derived from the master password using [Argon2id](#argon2id).
So together with a secure master password, it is unbreakable.

### RSA

[RSA](https://en.wikipedia.org/wiki/RSA_(cryptosystem)) is used to encrypt data that is shared with other users.
The public key and private key are generated on the client side, and the public key and private key are sent to the server.
But the private key is encrypted using the encryption key.
