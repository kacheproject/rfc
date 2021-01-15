# Profile

Profile is a small sqlite3 database keeps:

- Basic Infomation
- Signing keys
- Vault details (id, name, tree_decryption_key, tree_encryption_key, encryption_key, decryption_key, access_key, owner, directory_server)

## Userlets and Systemlets
Profiles have tables `userlets` and `systemlets`, which are under key-vaule structure. The `systemlets` table keeps infomation about the database, for example, `version`. The `userlets` store user infomation.

## Basic Infomation
These keys must be presented in `userlet`:
- username
- id
- signing_key

## System Infomation
These keys must be presented in `systemlet`:
- version (currently, it's `1`.)

## Vaults
Profile saves all vaults user can access, they are saved in `vaults`:
- id
- owner_id
- content_pub
- content_pri
- tree_pub
- tree_pri
- directory_server
- salt

## Signing
Signing is the only way in kache to check the profile's identity. Ed25519 system is being used.
The user's private key is saved in `userlets` as `signing_key`.

## Synchronizing between Devices
Kache uses standard method to synchronize profile between devices. For every profile, a vault call "profile+[id]" must be created and added to the profile, for example `profile+39db07ce-d436-4e0e-a88c-bfeb8950d9f3`.

There will be a "change stack" on every client which require synchronizing. It stores every change since the profile synchronized with any other client. Before one client apply changes on the profile in the vault, it must synchronize the profile from others. Clients should declare the changes on the profile on the directory server after change stack applied. The stack will be cleaned after the changes applied successfully.

Besides the profile in vault, the implementation can work on a copy which is appiled the changes instantly for simple code.