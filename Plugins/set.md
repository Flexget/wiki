= Set =

Stores info in an entry

'''Example:'''

{{{
set:
  path: ~/torrents/
}}}

== Advanced ==

=== Set as a sub-plugin ===

Set is not really that useful at the feed level. Certain plugins enable set commands to be called for a specific subset of entries from a feed. Currently regexp and series support this format. The use of set in these cases is best understandable through examples.
 To set the stop ratio option for Some Show:
{{{
series:
  - Some Show:
      set:
        ratio: 2.0
}}}
 This example will set the label for this regexp, but not that regexp.
{{{
regexp:
  accept:
    - this regexp:
        set:
          label: pizza
    - that regexp
}}}

=== String Replacement === #string-replacement

The set plugin also performs another useful function which can dynamically change an option for each entry accepted by a feed. Using the [http://docs.python.org/library/stdtypes.html#string-formatting-operations python string replacement] format, a variable from an [wiki:Entry entry] can be substituted into your set option. This can also be explained through an example.
 This example uses string replacement to place shows in series 'groupa' in their own show title and season folders.
{{{
series:
  settings:
    groupa:
      set:
        movedone: /home/usera/TV/%(series_name)s/Season %(series_season)d/
  groupa:
    - Some Show
    - Some Other Show
}}}

=== Plugins that accept Set keywords ===

Calling set however does not do much unless another plugin uses the information you have set. The following plugins will use values you have set with this plugin.

'''[wiki:Plugins/deluge Deluge]'''

 * {{{path}}}
 * {{{movedone}}}
 * {{{label}}}
 * {{{queuetotop}}}
 * {{{addpaused}}}
 * {{{maxupspeed}}}
 * {{{maxdownspeed}}}
 * {{{maxconnections}}}
 * {{{maxupslots}}}
 * {{{ratio}}}
 * {{{removeatratio}}}
 * {{{compact}}}
 * {{{automanaged}}}
 * {{{content_filename}}}

'''[wiki:Plugins/transmissionrpc Transmissionrpc]'''

 * {{{path}}}
 * {{{addpaused}}}
 * {{{maxconnections}}}
 * {{{maxupspeed}}}
 * {{{maxdownspeed}}}
 * {{{ratio}}}

'''[wiki:Plugins/download Download]'''

 * {{{path}}}

Options configured from the set plugin will override configuration values set directly in the plugin that is reading them.

