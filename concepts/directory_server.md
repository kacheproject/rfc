# Directory Server
Directory server holds infomation about vaults and profiles.

## Vaults
Directory server holds many details about vaults to provide friendly user experience, including:

- Tree of files (optionally encrypted)
- Unique ID

### How tree will be saved
Tree keeps paths. For every path, two things will be saved: (plain-text or encrypted) path and hash of the path.

### Encrypted tree
Many cheap chip does not have AES hardware which can speed up decryption and encryption process to 6Gb/s (typical). And for most user it is no worth to protect the file names, beacuse it leak little infomation. It's not everyone needed feature and it will cost much when you don't need. So the encrypted tree for vaults must be disable by default.

When this feature on, the paths of the tree must be encrypted by XSalsa20 and Poly1305 MAC (it's default of libsodium's public-key cryptography) with 256 bits key. Profile should keep the private key.

### How to access files
Directory server store all the trees of all vaults, but the path should not expose to clients which without permission. Directory server would return the hash of files which you requested for. And you can use that "file hash" with the request key of vault to request the file content from other clients.

## Profiles
Only when user request to store profile database to download it on another device, directory server will accept the random file and expose to any client which have specific string for a limited time.

Directory server still saves signing public key and unique id for profile to identify the user has permission.
