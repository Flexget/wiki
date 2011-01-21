= Set =

Stores info in an [wiki:Entry entry]. Can also do dynamic formatting per entry.

'''Example:'''

{{{
set:
  path: ~/torrents/
}}}

== Set as a sub-plugin ==

Set is not really that useful at the feed level. Certain plugins enable set commands to be called for a specific subset of entries from a feed. Currently [wiki:Plugins/regexp regexp] and [wiki:Plugins/series series] support this format. The use of set in these cases is best understandable through examples.
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

== Dynamic Formatting ==

The set plugin peforms another useful function in that it can dynamically format it's values based on other [wiki:Entry entry fields]. There are two methods for this, using the more powerful jinja2 template system, or if jinja2 is not available, simple replacement can be done with python string replacement.

=== Jinja2 Templates ===

Use [http://jinja.pocoo.org/templates/ jinja2 template] strings to create or modify [wiki:Entry entry fields].

'''NOTES:'''
 - All the fields from the entry are available in the jinja template context.
 - You can use [http://jinja.pocoo.org/templates/#builtin-filters jinja filters] to do formatting on fields from the entry.
 - If a referenced field is not available, the target field will be set to an empty string. If you would like to change this, you can use the jinja 'default' filter.

'''Example:'''

This example sets the {{{content_filename}}} using the information parsed by the [wiki:Plugins/series series] plugin. The [wiki:Plugins/deluge deluge] plugin uses the {{{content_filename}}} field to rename a file inside the torrent.
{{{
set:
  content_filename: "{{ series_name|replace(' ','.') }}.{{ series_id }}.{{ quality|upper }}{% if proper %}-proper{% endif %}"
}}}
This will result in filenames like: The.Show.S02E03.HDTV.avi and Other.Show.S02E04.720P-proper.mkv

=== String Replacement === #string-replacement

Using the [http://docs.python.org/library/stdtypes.html#string-formatting-operations python string replacement] format, a variable from an [wiki:Entry entry] can be substituted into your set option.

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
 * {{{addpaused}}}
 * {{{maxconnections}}}
 * {{{maxupspeed}}}
 * {{{maxdownspeed}}}
 * {{{ratio}}}

'''[wiki:Plugins/download Download]'''

 * {{{path}}}

Options configured from the set plugin will override configuration values set directly in the plugin that is reading them.

