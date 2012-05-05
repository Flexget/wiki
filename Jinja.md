= Jinja2 Templating =

Some options can have dynamically formatted values based on other [wiki:Entry entry fields]. This is done using the powerful [http://jinja.pocoo.org/templates/ jinja2 template] system to create or modify [wiki:Entry entry fields].

'''NOTES:'''

- All the fields from the entry are available in the jinja template context.
- {{{now}}} is also available, which is a python datetime object representing the current time.
- You can use [http://jinja.pocoo.org/templates/#builtin-filters jinja filters] to do formatting on fields from the entry.
- If a referenced field is not available, the target field will be set to an empty string. If you would like to change this, you can use the jinja 'default' filter.

'''Example:'''

This example sets the {{{content_filename}}} using the information parsed by the [wiki:Plugins/series series] plugin. The [wiki:Plugins/deluge deluge] plugin uses the {{{content_filename}}} field to rename a file inside the torrent.

{{{
set:
  content_filename: "{{ series_name|replace(' ','.') }}.{{ series_id }}.{{ quality|upper }}{% if proper %}-proper{% endif %}"
}}}

This will result in filenames like: The.Show.S02E03.HDTV.avi and Other.Show.S02E04.720P-proper.mkv

=== Jinja2 Filters ===

When using Jinja2 templates, you can use the following custom filters in addition to the [http://jinja.pocoo.org/templates/#builtin-filters built-in ones].

 pad(length):: Pad a number with 0s to the specified length.
 pathbase:: Base name of a path.
 pathname:: Base name of a path, without its extension.
 pathext:: Extension of a path (including the '.').
 pathdir:: Directory containing the given path.
 pathscrub(ascii=False, windows=<currentos>):: Replace problematic characters in a path. {{{windows}}} can be forced to True to replace invalid characters in Windows paths. \\ '''NOTE:''' This should rarely be needed due to the builtin [wiki:Plugins/pathscrub pathscrub] plugin.
 re_replace(pattern, replacement):: Do regexp substitution on the string.
 formatdate(format):: Do string formatting on datetime objects according to [http://docs.python.org/library/datetime.html#strftime-strptime-behavior strftime] {{{format}}} string.

Example:
{{{
set:
  # Replace filename by scrubbed title and keep the extension
  filename: '{{title | pathscrub}}{{filename | pathext}}'
}}}