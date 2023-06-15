# Security

## What does the server store?

The server only stores data that is encrypted on the local device before sending it. So your secrets are safe and always yours!

## How does the encryption work?

The encryption process follows the steps outlined below:

1. **Key Generation:**
    - The private key is derived from the password hash using the Argon2id algorithm.
    - Argon2id is configured with the following default parameters:
        - Memory: 64 MB
        - Iterations: 4
        - Parallelism: 3
        - Salt: User email
        - Hash Length: 32 bytes
    - Curve25519 elliptic curve is used for the key exchange.
    - The private key and public key (or the second user's public key) are used to generate a shared secret.

2. **Data Encryption:**
    - AES GCM 256-bit algorithm is employed for data encryption.
    - The shared secret generated in the previous step is used as the encryption key.
    - The data is encrypted using the AES GCM algorithm with the generated key.

3. **Transmitting the Encrypted Data:**
    - The encrypted data is then sent to the server.
    - As the server only stores encrypted data, the confidentiality of your information is maintained.

Please note that this is a simplified explanation of the encryption process, highlighting the key steps involved in securing your data.
