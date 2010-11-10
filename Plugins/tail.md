= Tail =

Similar to the [wiki:Plugins/text text] plugin but remembers the file position and continues from it. This plugins does NOT work for log files that are rotated.

'''Example:'''

{{{
tail:
  file: ~/irclogs/some/log
  entry:
    title: 'TITLE: (.*) URL:'
    url: 'URL: (.*)'
}}}