# Vault

Vault is a virtual root for any case.

- It's identified by unique id.
- Every vault have its own key pair for encryption.
- Encryption is done by application.
- Any vault is not linked to profile.

Vaults is used to isolate application's saving. Any file in kache must saved in one or more vault.

## On Storage Servers
Storage servers save the files indexed by the hashes of path.

## On Directory Servers
Directory server keeps the whole tree of vault with optionally encrypted.

## On Clients
Clients (including storage servers) use a rsync-like protocol to exchange files. Clients are responsible to keep the tree in sync with directory server.
