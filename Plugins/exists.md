# Exists
Reject entries if same filename or directory already exists in given path (recursively).

## Example:
```
exists: /some/storage/path/
```


Multiple paths can be specified as a list:

```
exists:
  - /some/storage/path/
  - /another/storage/path/
```


''Note: As of version 1.1.98 plugin will follow symbolically linked directories.
''