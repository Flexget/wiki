= Format Field =
This plugin lets you use [http://jinja.pocoo.org/ jinja2] template strings to create or modify [wiki:Entry entry fields]. This is similar to the [wiki:Plugins/set set] plugin, but allows for more advanced formatting.

'''NOTES:'''
 - All the fields from the entry are available in the jinja template context.
 - You can use [http://jinja.pocoo.org/templates/#builtin-filters jinja filters] to do formatting on fields from the entry.
 - If a referenced field is not available, nothing will be inserted, but the template rendering will still succeed.

=== Example ===
This example sets the {{{content_filename}}} using the information parsed by the [wiki:Plugins/series series] plugin. The [wiki:Plugins/deluge deluge] plugin uses the {{{content_filename}}} field to rename a file inside the torrent.
{{{
format_field:
  content_filename: |
    {{ series_name|replace(' ','.') }}.{{ series_id }}.{{ quality|upper }}{% if proper %}-proper{% endif %}
}}}
This will result in filenames like: The.Show.S02E03.HDTV and Other.Show.S02E04.720P-proper