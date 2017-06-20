# Url Rewriter for rmz.cr
Read [how URL rewriting works](/URLRewriters).

The feed from rmz.cr only gives links to an indexing page which then contains the actual download links. This plugin grabs the download links from rmz.cr and rewrites the `url` field to the first link that is found.

If more than one valid link is found, the plugin puts them as an array into the `urls` field of the entry.

You can filter links to which filehosters should be grabbed by adding regular expressions to the `filehosters_re` configuration parameter.

**Example:**

```yaml
  rmz:
    filehosters_re:
      - domain\.com
      - domain2\.org
```

Assuming there are the following links on the rmz.cr download page:

```html
http://domainx.cr/CoolFile.avi
http://domain2.org/CoolFile.avi
http://domain.com/CoolFile.part1.avi
http://domain.com/CoolFile.part2.avi
```
The plugin would rewrite the `url` field of the entry to:
```html
http://domain2.org/CoolFile.avi
```
and would add the `urls` field containing an array of links:
```html
['http://domain2.org/CoolFile.avi',
'http://domain.com/CoolFile.part1.avi',
'http://domain.com/CoolFile.part2.avi']
```
Particularly in case the files are split into multiple parts, it is recommended that you configure your output to use the `urls` field of the entry.

**Example for JDownloader 2 (using the folderwatch extension):**
```yaml
  exec:
    - echo "text={{urls}}" >> "/path/to/jd2/folderwatch/{{title}}.crawljob"
```