= Set =

Stores info in an entry

'''Example:'''

{{{
set:
  path: ~/torrents/
}}}

== Advanced ==

Set is not really that useful at the feed level. Certain plugins enable set commands to be called for a specific subset of entries from a feed. Currently regexp and series support this format. The use of set in these cases is best understandable through an example.

{{{
series:
  - Some Show:
      set:
        path: /download/here/
}}}
{{{
regexp:
  accept:
    - some regexp:
        set:
          path: /download/there/
    - another regexp
}}}

Calling set however does not do much unless another plugin uses the information you have set.
Mostly useful for deluge plugin which will utilize certain values, here are the available keywords:

'''[wiki:OutputDeluge deluge:]'''
Will read {{{path}}}, {{{movedone}}}, {{{label}}} and {{{queuetotop}}} from set, set info will override those deluge configuration values with the set values.

Set will throw errors if you attempt to set keywords not supported by any of your loaded plugins for the feed.