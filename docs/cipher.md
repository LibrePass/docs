# Cipher

The cipher is every entry added to the vault in LibrePass. It can be a login, a secure note, or a card.

## EncryptedCipher

`EncryptedCipher` represents an encrypted cipher stored in the database.

### Fields:
- `id`: Cipher identifier.
- `owner`: Owner identifier.
- `type`: Cipher type (numeric value corresponding to the type in [CipherType](#ciphertype)).
- `protectedData`: Encrypted cipher data.
- `collection`: Collection identifier.
- `favorite`: Whether the cipher is marked as a favorite.
- `rePrompt`: Whether the password should be re-prompted (UI feature only).
- `version`: Cipher version (currently 1).
- `created`: Creation date.
- `lastModified`: Last modified date.

## Cipher

`Cipher` represents a single cipher entry.

### Fields:
- `id`: Cipher identifier.
- `owner`: Owner identifier.
- `type`: Cipher type - [CipherType](#ciphertype).
- `loginData`: Login data (only if the cipher is of type "Login") - [CipherLoginData](#cipherlogindata).
- `secureNoteData`: Secure note data (only if the cipher is of type "SecureNote") - [CipherSecureNoteData](#ciphersecurenotedata).
- `cardData`: Card data (only if the cipher is of type "Card") - [CipherCardData](#ciphercarddata).
- `collection`: Collection identifier.
- `favorite`: Whether the cipher is marked as a favorite.
- `rePrompt`: Whether the cipher should be re-prompted (UI feature only).
- `version`: Cipher version (currently 1).
- `created`: Creation date.
- `lastModified`: Last modified date.

## CipherType

`CipherType` is an enum class representing the type of cipher.

Values:
- `Login`: Login cipher type.
- `SecureNote`: Secure note cipher type.
- `Card`: Card cipher type.

## Cipher data

### CipherLoginData

`CipherLoginData` contains login data for a "Login" type cipher.

#### Fields:
- `name`: Cipher name.
- `username`: Login username (can be null).
- `password`: Login password (can be null).
- `passwordHistory`: Password history, a list of `PasswordHistory` objects.
- `uris`: List of login-related URIs.
- `twoFactor`: Two-factor authentication secret.
- `notes`: Notes for the cipher.
- `fields`: Custom fields, represented as a list of `CipherField` objects.

#### PasswordHistory

`PasswordHistory` represents password history in `CipherLoginData`.

#### Fields:
- `password`: Password.
- `lastUsed`: Date when the password was last used.

### CipherSecureNoteData

`CipherSecureNoteData` contains secure note data for a "SecureNote" type cipher.

#### Fields:
- `title`: Note title.
- `note`: Secure note content.
- `fields`: Custom fields, represented as a list of `CipherField` objects.

### CipherCardData

`CipherCardData` contains card data for a "Card" type cipher.

#### Fields:
- `cardholderName`: Cardholder name.
- `brand`: Card brand (can be null).
- `number`: Card number (can be null).
- `expMonth`: Card expiration month (can be null).
- `expYear`: Card expiration year (can be null).
- `code`: Card CVV code (can be null).
- `notes`: Notes for the card.
- `fields`: Custom fields, represented as a list of `CipherField` objects.

### CipherField

`CipherField` represents a custom field in a cipher.

#### Fields:
- `name`: Field name.
- `type`: Field type (enum value of `CipherFieldType`: Text, Hidden).
- `value`: Field value.

### CipherFieldType

`CipherFieldType` is an enum class representing the type of a cipher field.

Values:

- `Text`: Text field.
- `Hidden`: Hidden field.
