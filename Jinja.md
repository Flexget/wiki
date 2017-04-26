# Jinja2 Templating

<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  Advanced use. Not required for most things.
</div>

Some options can have dynamically formatted values based on other [entry fields](/Entry). This is done using the powerful [jinja2 template](http://jinja.pocoo.org/docs/templates/) system to create or modify [entry fields](/Entry).

**NOTES:**

- All the fields from the entry are available in the jinja template context.
- `now` is also available, which is a python datetime object representing the current time.
- You can use [jinja filters](http://jinja.pocoo.org/docs/templates/#builtin-filters) to do formatting on fields from the entry.
- If a referenced field is not available, the target field will be set to an empty string. If you would like to change this, you can use the jinja 'default' filter.

#### Example:

This example sets the `content_filename` using the information parsed by the [series](/Plugins/series) plugin. The [deluge](/Plugins/deluge) plugin uses the `content_filename` field to rename a file inside the torrent.

```yaml
set:
  content_filename: "{{ series_name|replace(' ','.') }}.{{ series_id }}.{{ quality|upper }}{% if proper %}-proper{% endif %}"
```

This will result in filenames like: The.Show.S02E03.HDTV.avi and Other.Show.S02E04.720P-proper.mkv

### Jinja2 Filters
**Note**: To get up-to-date information about all available Jinja filters, use the following ClI command:
```bash
flexget jinja-filters
```

When using Jinja2 templates, you can use the following custom filters in addition to the [built-in ones](http://jinja.pocoo.org/docs/dev/templates/#builtin-filters).

|Name|Description|
|---|---|
|`pad(length)`| Pad a number with 0s to the specified length|
|`pathbase`|Base name of a path.|
|`pathname`|Base name of a path, without its extension.|
|`pathext`|Extension of a path (including the '.').|
|`pathdir`| Directory containing the given path.|
|`pathscrub(os)`| Replace problematic characters in a path. If os parameter is omitted, the current os, or os defined by [pathscrub](/Plugins/pathscrub) plugin will be used.<br> **NOTE:** This should rarely be needed due to the builtin [pathscrub](/Plugins/pathscrub) plugin.
|`re_replace(pattern, replacement)`| Do regexp substitution on the string.<br> **NOTE:** Captured groups can be accessed in the replacement string by using backreferences:<br>- `\\1` when enclosed with apostrophes or `\\\\1` when enclosed with quotes<br>- `\g<1>` when enclosed with either apostrophes or quotes|
|`formatdate(format)`| Do string formatting on datetime objects according to [strftime](http://strftime.org/).|
|`re_search(pattern)`|Perform a search for given regexp pattern, return the matching portion of the text.
|`parsedate`|Attempts to parse a date according to the rules in RFC 2822
|`format_number`|Formats a number according to the user's locale.
|`to_date`|Formats date



#### Example:

```yaml
set:
  # Replace filename by title and keep the extension
  filename: '{{title}}{{filename | pathext}}'
```
