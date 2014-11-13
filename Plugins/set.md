= Set =

Stores info in an [wiki:Entry entry]. Can also do dynamic formatting per entry.

'''Example:'''

{{{
set:
  path: ~/torrents/
}}}

== Set as a sub-plugin ==

Set is not really that useful at the task level. Certain plugins enable set commands to be called for a specific subset of entries from a task. Currently [wiki:Plugins/regexp regexp] and [wiki:Plugins/series series] support this format. The use of set in these cases is best understandable through examples.
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

[[Include(wiki:Jinja)]]

== Plugins that accept Set keywords ==

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

'''[wiki:Plugins/transmission Transmission]'''

 * {{{path}}}
 * {{{content_filename}}}
 * {{{addpaused}}}
 * {{{maxconnections}}}
 * {{{maxupspeed}}}
 * {{{maxdownspeed}}}
 * {{{ratio}}}

'''[wiki:Plugins/download Download]'''

 * {{{path}}}
 * {{{filename}}}

Options configured from the set plugin will override configuration values set directly in the plugin that is reading them.
