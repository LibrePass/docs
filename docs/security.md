# Security

## Server

The server only stores data that is encrypted on the local device before sending it.
So your secrets are safe and always yours!

## KDF Algorithm (Key Derivation Function)

LibrePass first derives a key from your master password using the [Argon2](https://en.wikipedia.org/wiki/Argon2) algorithm.
This key is then used to decrypt the encryption key which is retrieved from the server in encrypted form.
Before sending the key to the server, it has additional iterations using [PBKDF2-SHA256](https://en.wikipedia.org/wiki/PBKDF2)
because the earlier key was used for encryption key encryption.

## Argon2id

LibrePass uses the Argon2id variant of Argon2. This variant is resistant to side-channel attacks and GPU cracking.

### Default Parameters (client-side)

Client-side parameters are used to derive the key for encryption key encryption.
They are not sent to the server. Sent to the server is the key after additional [PBKDF2-SHA256](#pbkdf2-sha256) iterations.

| Parameter   | Value        |
|-------------|--------------|
| Memory      | 64 MB        |
| Iterations  | 4            |
| Parallelism | 3            |
| Salt        | (user email) |
| Hash Length | 32 bytes     |

### Server Parameters (server-side)

Server-side parameters are used to compute a hash that is stored in the database.

| Parameter   | Value    |
|-------------|----------|
| Memory      | 15 MB    |
| Iterations  | 1        |
| Parallelism | 1        |
| Salt        | 32 bytes |
| Hash Length | 32 bytes |

## PBKDF2-SHA256

PBKDF2-SHA256 is used to derive the final password hash, which is sent to the server to authenticate the user.
It is computed from the hash after [Argon2id](#argon2id) iterations.

| Parameter   | Value        |
|-------------|--------------|
| Iterations  | 500          |
| Salt        | (user email) |
| Hash Length | 32 bytes     |
