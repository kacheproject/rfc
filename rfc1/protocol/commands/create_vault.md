# `create_vault`

````
vault_name = string signed by profile's signing private key
tree_encryption_key = empty | 256 bits key # empty means disable this feature
create_vault = $, profile_id, vault_id, vault_name, tree_encryption_key 
REPLY create_vault = "OK", vault_public_key, vault_private_key, vault_tree_encryption_key
REPLY create_vault = "ERROR", error_code, error_message
````

- `profile_id` is the profile id of the onwer to be
- `vault_id`, a UUID of the new vault
- `vault_name`: string signed by profile's signing private key
- `tree_encryption_key` is the key to encrypt the tree
