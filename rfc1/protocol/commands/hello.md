# `hello`

Say hello to each other. This command is requested by the "connect"-side.

````
hello = $, api_version, name, software, supported_feature_sets
REPLY hello = "hello", api_version, name, software, supported_feature_sets
````

- `api_version` is the RFC number. Currently is `202101`.
- `name` is the name which is set by owner. For example `my_directory_server"
- `software` is a string to identify the software used in this connection. It looks like `SoftwareName/Version`, for example `kache/0.1`. It's no need to include detailed version for security reason.
- `supported_feature_set` is a comma-separated string to suggest the features that the software supported.
