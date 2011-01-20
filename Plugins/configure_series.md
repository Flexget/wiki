= Import series =

Generates [wiki:Plugins/series series] plugin configuration from any (upgraded) input.

'''Syntax:'''

{{{
import_series:
  [settings]:
    # any series option
  from:
    # any input
}}}

'''Example:'''

Lets say you have a directory where all your series are stored in each in the own folder. Something like:

{{{
/media/series/name of series/
/media/series/name of series/
/media/series/name of series/
}}}

To automatically configure series plugin with all these you could do following:

{{{
import_series:
  settings:
    quality: 720p
  from:
    listdir:
      - /media/series/
}}}
