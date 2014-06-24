= Move =

''TODO: Improve documentation''

Syntax:

{{{
move:
  [to]: directory to move accepted entries to, allows value replacement, defaults to download path
  [filename]: the actual filename inside the 'to' directory to name the entries, allows value replacement
  [allow_dir]: allows or denies to operate on entries pointing to directories
  [unpack_safety]: enable or disable unpacking safety checks, enabled by default. causes 1 sec delay per processed entry
  [clean_source]: delete source directory if it has less MB left than given after move
  [along]: Move additional files such as subtitles
}}}

[] = optional

Entry field "to" can be used to override given path.

Here is an example of usage in a more comprehensive context

{{{
tasks:
  move-episodes:
    metainfo_series: yes 
    accept_all: yes 
    find:
      path: /filestorage1/
      recursive: yes 
    move:
      to: "/filestorage2/{{series_name}}/"
      filename: '{{ series_name }} - {{ series_id }}{{ location|pathext }}'
      along:
        - sub
        - srt
}}}

It is important to note that the files are moved as single files and no checks are made if multiple files match the same name. The files already present in the directory (even if moved during the same pass) are overwritten.