# Vault

Vault is a key-value database which presents a isolation.

- Identified by unique identity
- Encrypted by default
- Doesn't be linked to profile
- Being synchronised across devices

## Common Fields
All vaults must contain these fields:
- `name` is the name of vault
- `version` is the version of the vault, current is string `1`

## Storage Vault
Storage vault is a standard format to save files in a genernal style.
It requires these fields:
- `tree` is the id of the linked resource tree
- `pool` is the file pool id for files
- `tree_key` and `tree_key_pub`, the pair of encryption key for tree
- `file_key` and `file_key_pub`, the pair of encryption key for file contents
- `tree_hash_salt`, the salt used to salt the hash in tree
