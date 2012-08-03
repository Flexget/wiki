= Move =

''TODO: Improve documentation''

Syntax:

{{{
move:
  [to]: directory to move accepted entries to, allows value replacement, defaults to download path
  [filename]: the actual filename inside the 'to' directory to name the entries, allows value replacement
  [unpack_safety]: enable or disable unpacking safety checks, enabled by default. causes 1 sec delay per processed entry
  [clean_source]: delete source directory if it has less MB left than given after move
}}}

[] = optional

Entry field "to" can be used to override given path.

Here is an example of usage in a more comprehensive context

{{{
feeds:
  move-episodes:
    metainfo_series: yes 
    thetvdb_lookup: yes 
    accept_all: yes 
    find:
      path: /filestorage1/
      recursive: yes 
    move:
      to: "/filestorage2/{{series_name}}/"
      filename: '{{ series_name }} - {{ series_id }}{{title | pathext}}'
}}}

It is important to note that the files are moved as single files and no checks are made if multiple files match the same name. The files already present in the directory (even if moved during the same pass) are overwritten.