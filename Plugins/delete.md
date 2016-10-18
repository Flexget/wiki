# Delete
*TODO: Improve documentation*

Syntax:

```code
delete:
  [allow_dir]: allows or denies to operate on entries pointing to directories
  [along]: delete additional files such as subtitles
    [extensions]: file extensions
    [subdirs]: sub directories to search in
  [clean_source]: delete source directory if it has less MB left than given after delete
```

[] = optional

Here is an example of usage in a more comprehensive context (untested)

```yaml
tasks:
  cleanup:
    filesystem:
      path: /filestorage1/
      recursive: yes
    age:
      field: created
      action: accept
      age: 600 days
    delete:
      clean_source: 1
      along:
        extensions:
          - sub
          - srt
```
