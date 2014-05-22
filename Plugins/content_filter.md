= Content Filter =
This allows filtering based on the filenames inside of torrents. You can specify either an acceptable file mask, a file mask to reject, or both. You can also specify a list of masks for either option.

'''Note:''' content_filter doesn't work with magnet links, as it works by analyzing the file list present in the .torrent file. You can include the [wiki:Plugins/magnets magnets] plugin to reject any magnet entries.

''' Example '''

{{{
content_filter:
  require: '*.avi'
}}}

Rejects torrents that do not have avi file in them.

''' Example '''

{{{
content_filter:
  reject: '*.rar'
}}}

Reject torrents that have rars in them.

''' Example '''

{{{
content_filter:
  require:
    - '*.avi'
    - '*.mkv'
  reject: '*.wmv'
}}}

Reject torrent if it doesn't have avi OR mkv in it. Reject also if there are wmv files.

''' Example '''

{{{
content_filter:
  require_all: 
    - '*.mkv'
    - '*.nfo'
}}}

Reject torrents that don't have a matroska container AND a nfo file.

''' Example '''

{{{
content_filter:
  require_mainfile: yes
}}}

Reject multifile torrents that don't have one file at least 90% of total size (single-file torrents are not affected).
