# Copy
*TODO: Improve documentation*

Syntax:

```
copy:
  [to]: directory to copy accepted entries to, allows value replacement, defaults to download path
  [filename]: the actual filename inside the 'to' directory to name the entries, allows value replacement
  [allow_dir]: allows or denies to operate on entries pointing to directories
  [unpack_safety]: enable or disable unpacking safety checks, enabled by default. causes 1 sec delay per processed entry
  [along]: Copy additional files such as subtitles
    [extensions]: file extensions
    [subdirs]: sub directories to search in
```

[] = optional

Entry field "copy_to" can be used to override given path.

Here is an example of usage in a more comprehensive context

```
tasks:
  copy-episodes:
    metainfo_series: yes 
    accept_all: yes 
    filesystem:
      path: /filestorage1/
      recursive: yes 
    copy:
      to: "/filestorage2/{{series_name}}/"
      filename: '{{ series_name }} - {{ series_id }}{{ location|pathext }}'
      along:
        extensions:
          - sub
          - srt
```

It is important to note that the files are copied as single files and no checks are made if multiple files match the same name. The files already present in the directory (even if copied during the same pass) are overwritten.