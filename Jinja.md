---
title: Jinja
description: 
published: true
date: 2023-07-16T17:47:27.061Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:50:14.756Z
---

# Jinja2 Templating

> Advanced use. Not required for most things.
{.is-info}

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
**Note**: To get up-to-date information about all available Jinja filters, use the following CLI command:
```bash
flexget jinja-filters
```

When using Jinja2 templates, you can use the following custom filters in addition to the [built-in ones](http://jinja.pocoo.org/docs/dev/templates/#builtin-filters).

|Name|Description|
|---|---|
|`asciify`|Simplify a string replacing for example `à` with `a`, `õ` with `o` and `ç` with `c`
|`format_number`|Formats a number according to the user's locale.
|`formatdate(format)`| Do string formatting on datetime objects according to [strftime](http://strftime.org/).|
|`get_year`|Get year from end of string (for example: get year from the end of movie name)
|`pad(length)`| Pad a number with 0s to the specified length|
|`parsedate`|Attempts to parse a date according to the rules in RFC 2822
|`pathbase`|Base name of a path.|
|`pathdir`| Directory containing the given path.|
|`pathext`|Extension of a path (including the '.').|
|`pathname`|Base name of a path, without its extension.|
|`pathscrub(os)`| Replace problematic characters in a path. If os parameter is omitted, the current os, or os defined by [pathscrub](/Plugins/pathscrub) plugin will be used.<br> **NOTE:** This should rarely be needed due to the builtin [pathscrub](/Plugins/pathscrub) plugin.
|`re_replace(pattern, replacement)`| Do regexp substitution on the string.<br>**NOTE 1**: Case-sensitive. You can change this behaviour by starting your pattern with `(?i)`<br>- `'This MIGHT Match'|re_replace('might', 'WON’T')`<br>- `'This MIGHT Match'|re_replace('(?i)might', 'WILL')`<br>**NOTE 2:** Captured groups can be accessed in the replacement string by using backreferences:<br>- `\\1` when enclosed with apostrophes or `\\\\1` when enclosed with quotes<br>- `\g<1>` when enclosed with either apostrophes or quotes|
|`re_search(pattern)`|Perform a search for given regexp pattern, return the matching portion of the text.
|`strip_symbols`|Removes all special chars from a string, keeps accent words. The symbols are removed, only `()-_[].` and replaced by a `space`. Double `space` are also replaced by a single `space`
|`strip_year`|Removes year from end of string (for example: remove year from the end of movie name)
|`to_date`|Formats date


#### Example:

```yaml
set:
  # Replace filename by title and keep the extension
  filename: '{{title}}{{filename | pathext}}'
  # Create a simple title
  id_name: '{{title|asciify|strip_symbols}}'
```
### Jinja2 Tests
When using Jinja2 tests, you can use the following custom tests in addition to the [built-in tests](http://jinja.pocoo.org/docs/dev/templates/#list-of-builtin-tests).

|Name|Description|
|---|---|
|`is fs_file`|Check whether object is existing file (or symlink) in filesystem.|
|`is fs_dir`|Check whether object is existing directory (or symlink) in filesystem.|
|`is fs_link`|Check whether object is existing symlink in filesystem.|
#### Example:

```YAML
if:
  # check whether torrent file is in incomplete directory
  - ('/path/torrents/incomplete' ~ title) is fs_file: reject
```
