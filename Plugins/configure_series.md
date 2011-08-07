= Import series =

Generates [wiki:Plugins/series series] plugin configuration from any (upgraded) input. Using this doesn't prevent configuring [wiki:Plugins/series series] plugin additionally. 

Most commonly used with [wiki:/Plugins/thetvdb_favorites thetvdb_favorites] or [wiki:Plugins/listdir listdir].


'''Syntax:'''

{{{
import_series:
  [settings]:
    # any series option
  from:
    # any input(s)
}}}

'''Example with listdir:'''

Let's say you have a directory where all your series are stored in each in the own folder. Something like:

{{{
/media/series/pioneer one/
/media/series/south park/
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

This will make adding new series easy too, just create new directory there :)
