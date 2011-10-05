= Download =

Downloads content from entry url and writes it into a file. As default html response is considered as a download failure.

'''Example:'''

{{{
download: ~/torrents/
}}}

This is the most common use, there are additional options and features for more fine control.

== Download path (advanced) ==

Some plugins set download path per entry.
One such example is [wiki:Plugins/regexp regexp] that can be used to override path.

Example with alternative paths:

{{{
regexp:
  accept:
    - pattern1
    - pattern2
    - pattern3: ~/another_location/
download: ~/torrents/
}}}

This results that entries matching patterns 1 and 2 are saved into
~/torrents/ and pattern3 is saved to ~/another_location/. 
In the background this works by setting [wiki:Entry entries] matching pattern3 field `path` to `~/another_location/`.

For even more customization you can use [wiki:Plugins/set set] plugin to manually construct path to whatever you like.

'''Example'''

{{{
series:
  - pioneer one
set:
  path: /home/usera/TV/{{series_name}}/Season {{series_season}}/
download: yes
}}}

Note that in this example we did not specify path for download as we expect every entry to have a download `path`. If entry without `path` is tried to be downloaded it will be marked as failed.

== Options (advanced) ==

There are a couple of options that can be specified when using full syntax:

{{{
download:
  path: /path/here
  overwrite: yes
  fail_html: no
}}}

{{{overwrite}}} If a non-identical file already exists with the given name, it will be overwritten. (defaults to false)[[BR]]
{{{fail_html}}} If html content is recieved (usually a login page), fail the entry. (defaults to true) 

== Multiple urls ==

Some plugins (currently only [wiki:Plugins/rss rss], see "group link" value) can store multiple urls, to be tolerant to broken urls. If several urls are available, they will be tried sequentially until one works.
