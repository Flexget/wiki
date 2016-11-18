# Move
*TODO: Improve documentation*

### Syntax:

```text
move:
  [to]: directory to move accepted entries to, allows value replacement, defaults to download path
  [rename]: the actual filename inside the 'to' directory to rename the entries, allows value replacement
  [allow_dir]: allows or denies to operate on entries pointing to directories
  [keep_extension]: Enable or disable automatic adding of extension (e.g. .torrent) to renamed file. Default: Yes
  [unpack_safety]: enable or disable unpacking safety checks, enabled by default. causes 1 sec delay per processed entry
  [clean_source]: delete source directory if it has less MB left than given after move
  [along]: Move additional files such as subtitles
    [extensions]: file extensions
    [subdirs]: sub directories to search in
```

[] = optional

Entry field `move_to` can be used to override given path per entry basis.

### Examples

#### Organize series

```yaml
tasks:
  move-episodes:
    metainfo_series: yes 
    accept_all: yes 
    filesystem:
      path: /downloads/
      recursive: yes 
    move:
      to: '/storage/{{series_name}}/'
      filename: '{{ series_name }} - {{ series_id }}{{ location|pathext }}'
      along:
        extensions:
          - sub
          - srt
        subdirs:
          - Subs
```

It is important to note that the files are moved as single files and no checks are made if multiple files match the same name. The files already present in the directory (even if moved during the same pass) are overwritten.