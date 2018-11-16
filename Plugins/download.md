# Download
Downloads content from entry url and writes it into a file. As a default html response is considered as a download failure.

**Example:**

```yaml
download: ~/torrents/
```

This is the simplest use-case, there are additional options and features for more fine control.

### Download path (advanced)
Some plugins set download path per entry.
One such example is [regexp](/Plugins/regexp) that can be used to override path.

Example with alternative paths:

```yaml
regexp:
  accept:
    - pattern1
    - pattern2
    - pattern3: ~/another_location/
download: ~/torrents/
```

This results that entries matching patterns 1 and 2 are saved into
~/torrents/ and pattern3 is saved to ~/another_location/. 
In the background this works by setting [entries](/Entry) matching pattern3 field `path` to `~/another_location/`.

For even more customization you can use [set](/Plugins/set) plugin to manually construct path to whatever you like.

**Example**

```yaml
series:
  - pioneer one
set:
  path: '/home/usera/TV/{{series_name}}/Season {{series_season}}/'
download: yes
```

Note that in this example we did not specify path for download as we expect every entry to have a download `path`. If entry without `path` is tried to be downloaded it will be marked as failed.

### Filename (advanced)
You can also override filename that is saved by `filename` field. Here's an example that sets it based on title.

```yaml
set:
  filename: '{{title|pathscrub}}.torrent'
```

### Options (advanced)
There are a couple of options that can be specified when using full syntax:

```yaml
download:
  path: /path/here
  overwrite: yes
  fail_html: no
  temp: /path/for/temp
  filename: my_filename.torrent
```

|Option|Description|
|---|---|
|overwrite|If a non-identical file already exists with the given name, it will be overwritten. (defaults to false)|
|fail_html|If html content is recieved (usually a login page), fail the entry. (defaults to true)  |
|temp| Downloads are saved in a temporary location before being moved to their final path. You can override the default temporary folder with this option.  |
|filename| Overrides the original filename. Supports jinja replacement.|

### Multiple urls
Some plugins (ie. [rss](/Plugins/rss), see "group link" value) can store multiple urls, to be tolerant to broken urls. If several urls are available, they will be tried sequentially until one works.

### Authentication
If basic or digest authentication is needed, use the [download_auth](/Plugins/download_auth) for that.
