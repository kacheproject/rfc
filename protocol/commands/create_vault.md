# `create_vault`

````
vault_name = string signed by profile's signing private key
tree_encryption_key = empty | 256 bits key # empty means disable this feature
create_vault = $, profile_id, vault_id, tree_encryption_key 
REPLY create_vault = "OK", vault_public_key, vault_private_key, vault_tree_encryption_key
REPLY create_vault = "ERROR", error_code, error_message
````
