= Content Filter =
This allows filtering based on the filenames inside of torrents. You can specify either an acceptable file mask, a file mask to reject, or both. You can also specify a list of masks for either option.

''' Example '''
{{{
content_filter:
  require: '*.avi'
}}}
''' Example '''
{{{
content_filter:
  reject: '*.rar'
}}}
''' Example '''
{{{
content_filter:
  require:
    - '*.avi'
    - '*.mkv'
  reject: '*.wmv'
}}}