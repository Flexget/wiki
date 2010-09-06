= Download =

Downloads content from entry url and writes it into a file.

'''Example:'''

{{{
download: ~/torrents/
}}}

== Advanced ==

Some plugins may set alternative download path for entry.
Prime example is [wiki:Plugins/regexp regexp] that can be used to override path.

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

'''Multiple urls'''

Some plugins (currently only [wiki:Plugins/rss rss], see "group link" value) can store multiple urls, to be tolerant to broken urls. If several urls are available, they will be tried sequentially until one works.


'''Advanced Options'''

There are a couple of advanced options that can be specefied in this form:
{{{
download:
  path: /path/here
  overwrite: yes
  fail_html: no
}}}
{{{overwrite}}} If a non-identical file already exists with the given name, it will be overwritten. (defaults to false)[[BR]]
{{{fail_html}}} If html content is recieved (usually a login page), fail the entry. (defaults to true) 