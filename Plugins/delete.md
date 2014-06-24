= Delete =

''TODO: Improve documentation''

Syntax:

{{{
delete:
  [allow_dir]: allows or denies to operate on entries pointing to directories
  [along]: delete additional files such as subtitles
  [clean_source]: delete source directory if it has less MB left than given after delete
}}}

[] = optional

Here is an example of usage in a more comprehensive context

{{{
tasks:
  delete_old_stuff:
    find:
      path: /filestorage1/
      recursive: yes
    if:
      - timestamp and timestamp < now - timedelta(days=600): accept
    delete:
      clean_source: 1
      along:
        - sub
        - srt
}}}
