# Delete
*TODO: Improve documentation*

Syntax:

```
delete:
  [allow_dir](/allow_dir): allows or denies to operate on entries pointing to directories
  [along](/along): delete additional files such as subtitles
  [clean_source](/clean_source): delete source directory if it has less MB left than given after delete
```

[] = optional

Here is an example of usage in a more comprehensive context (untested)

```
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
        - sub
        - srt
```
