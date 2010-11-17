= Find =
This plugin searches through a directory (optionally recursively) and creates entries that match a file mask, or regexp.

''' Example '''

This example uses a file mask to list all torrents in a directory.
{{{
find:
  path: /home/me/incoming
  mask: '*.torrent'
}}}

''' Example '''

This example searches recursively and uses regexp to find any avi or mkv files. This input could be used in a sorting recipe.
{{{
find:
  path: /home/me/downloads
  regexp: '.*\.(avi|mkv)$'
  recursive: yes
}}}