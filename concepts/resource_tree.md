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
