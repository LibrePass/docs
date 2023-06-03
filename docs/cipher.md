# Cipher

## Encryption

Ciphers are encrypted using the encryption key using AES-CBC with a 256-bit key.
They are always stored and sent to the server in encrypted form.

## Example Cipher

The following is an example of a decrypted cipher object:

```json
{
  "id": "e31e264f-6624-47e9-a4cb-d6942e7ff215",
  "owner": "09c1efa8-cf85-4949-9716-ca69cae8f3d7",
  "type": 0,
  "data": {
    "name": "LibrePass",
    "username": "librepass@medzik.dev",
    "password": "Th3-V3ry-$3cure-P@ssw0rd",
    "uris": [
      "https://librepass.medzik.dev"
    ],
    "twoFactor": null,
    "notes": "Take control of your passwords with LibrePass.",
    "fields": [
      {
        "name": "Custom Field",
        "value": "Custom Value"
      }
    ]
  },
  "collection": null,
  "favorite": false,
  "rePrompt": false,
  "version": 1,
  "created": 1685122977,
  "lastModified": 1685122977
}
```

## Fields

| Field                | Type   | Description                                                   |
|----------------------|--------|---------------------------------------------------------------|
| id                   | UUID   | Unique identifier of the cipher.                              |
| owner                | UUID   | Unique identifier of the user who owns the cipher.            |
| [type](#cipher-type) | int    | Type of the cipher.                                           |
| [data](#cipher-data) | object | Cipher data.                                                  |
| collection           | UUID   | Unique identifier of the collection the cipher belongs to.    |
| favorite             | bool   | Whether the cipher is marked as favorite.                     |
| rePrompt             | bool   | Whether the password should be re-prompted. (Only UI-related) |
| version              | int    | Version of the cipher.                                        |
| created              | int    | Unix timestamp of the creation date.                          |
| lastModified         | int    | Unix timestamp of the last modification date.                 |

### Cipher Type

| Type | Description        |
|------|--------------------|
| 0    | Login Cipher       |
| 1    | Secure Note Cipher |
| 2    | Card Cipher        |

### Cipher Data

#### Login Cipher

| Field     | Type   | Description                                       |
|-----------|--------|---------------------------------------------------|
| name      | string | Name of the cipher.                               |
| username  | string | Username of the cipher.                           |
| password  | string | Password of the cipher.                           |
| uris      | array  | List of URIs associated with the cipher.          |
| twoFactor | string | Two-factor authentication code of the cipher.     |
| notes     | string | Notes of the cipher.                              |
| fields    | array  | List of custom fields associated with the cipher. |

#### Secure Note Cipher

| Field  | Type   | Description                                       |
|--------|--------|---------------------------------------------------|
| title  | string | Title of the cipher.                              |
| notes  | string | Notes of the cipher.                              |
| fields | array  | List of custom fields associated with the cipher. |

#### Card Cipher

| Field          | Type   | Description                                       |
|----------------|--------|---------------------------------------------------|
| cardholderName | string | Cardholder of the cipher.                         |
| brand          | string | Brand of the cipher.                              |
| number         | string | Number of the cipher.                             |
| expMonth       | int    | Expiration month of the cipher.                   |
| expYear        | int    | Expiration year of the cipher.                    |
| code           | string | Code of the cipher.                               |
| notes          | string | Notes of the cipher.                              |
| fields         | array  | List of custom fields associated with the cipher. |

### Custom Field

| Field | Type   | Description         |
|-------|--------|---------------------|
| name  | string | Name of the field.  |
| type  | int    | Type of the field.  |
| value | string | Value of the field. |

#### Custom Field Type

| Type | Description        |
|------|--------------------|
| 0    | Text Field         |
| 1    | Hidden Text Field  |
