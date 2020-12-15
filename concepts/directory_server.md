# Directory Server
Directory server holds infomation about vaults and profiles.

## Vaults
Directory server holds many details about vaults to provide friendly user experience, including:

- Tree of files (optionally encrypted)
- Unique ID

### How tree will be saved
For every path, three things will be saved: (plain-text or encrypted) path, hash of the path and the "block_id". Block id is a file hash which salted by vault-specific salt as the path hash.

### Encrypted tree
Encrypted tree is a recommended feature. It can be disable if user thinks their devices could not afford the performance cost.

The goal of encrypted tree is to prevent attacker visit the detailed paths without permissions.

When this feature on, the paths of the tree must be encrypted by XSalsa20 and Poly1305 MAC (it's default of libsodium's public-key cryptography) with 256 bits key. Profile should keep the private key.

### How to access files
Directory server store whole the trees of all vaults. As you request by the path hash, directory server would return the block ids which you requested for. And you can use that ids with the access request key of vault to request the file content from the other clients.

## Profiles
Only when user request to store profile database to download it on another device, directory server will accept the random file and expose to any client which have specific string for a limited time.

Directory server still saves signing public key and unique id for profile to identify the user has permission.
