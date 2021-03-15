# Resource Tree
Resource tree is a database for paths presents relative locations of resources.

- Linked to at least one vault
- Maintained by directory server
- Encrypted by special method

## How it constructed
````
| the hash (sha256 with salt) of path | encrypted path | encrypted value |
````
This method fits the use of relational database. We save the path's hash, secret text and the linked value to the tree. Genernally the value field saves the resource id in the linked pool.

## Resource Tree ID
Resource tree id combine the type identifier and a UUID v5, looks like:
````
restr+8a38bb79-b705-4cde-85e2-fa596ddd28b1
````
