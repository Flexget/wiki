# RSS
Parses any RSS feed.

## Simple configuration
```YAML
rss: <url>
```

Note: https supported.

### Authentication
**Basic http authentication**

```YAML
rss:
  url: <url>
  username: <name>
  password: <password>
```

Some feeds are private and require that you use some form of authentication, try [headers](/Plugins/headers) or  [cookies](/Plugins/cookies) plugins.

### Read from a file
You can also use local file instead of url.

**Example**

```YAML
rss:
  url: file:///path/to/rss/something.xml
```

## Advanced usages
There are more advanced options that can be used with the rss plugin if you need them.

### All Entries
By default this plugin outputs each entry from the rss on every run. If you would like to improve the performance of a task using this plugin, you can set `all_entries: no` to have each entry only created on the first run it is seen.

**Note:** Due to this behavior, the [only_new](/Plugins/only_new) plugin is not needed along with this input, and in fact should not be used, as it is less efficient.
```YAML
rss:
  url: http://example.com
  all_entries: no
```

### Link field
Incase RSS-feed uses some nonstandard field for `link` urls (ie. guid) you can
configure module to use url from any feedparser entry attribute.

**Example**

```YAML
rss:
  url: <url>
  link: guid
```

You can also configure link with a list of fields. This will cause the download, deluge, and transmission plugins to fall back to later urls if there is a problem with the first. This can be especially useful if you are using the deluge or transmission plugin, and your feed provides a magneturi field. This example falls back on a magnet link if there is an error grabbing the direct torrent download. 

**Example**

```YAML
rss:
  url: <url>
  link:
    - link
    - magneturi
```
**Note:** This example requires your feed provides the magneturi field, and that you are using an output plugin that can handle magnet uris.

### Title field
If you would like to use a different field from the rss as the title of the flexget entry, (or if your feed does not provide titles for the entries,) you can use the `title` option to specify any feedparser entry attribute.

**Example**
```YAML
rss:
  url: <url>
  title: date
```

### Silent mode
You can disable few possibly annoying warnings by setting `silent` value to `yes` on feeds where there are
frequently invalid items.

**Example**

```YAML
rss:
  url: <url>
  silent: yes
```

### Group Links
If the feed has several links by item, you can set the `group_links` value to `yes`. This way, only one entry will be generated for the item, with all links attached to it.
Links are fields given by the `link` value plus enclosures, in that order.

The download plugin will then try to download each link until one works.

**Example**

```YAML
rss:
  url: <url>
  group_links: yes
```

### Capture other fields
If you want to keep information in another rss field attached to the flexget [entry](/Entry), you can use the `other_fields` option.

**Example**
```YAML
rss:
  url: <url>
  other_fields:
    - date
```

If you want to remap the rss field to a different field in FlexGet, that is also possible. This can be useful for rss fields that contain special characters, like colons.

```yaml
rss:
  url: "<url>"
  other_fields:
    - "some:rssfield": the_flexget_field
```

### Convert to ASCII
Some feeds contain unicode characters which may cause problems. To force these into ASCII (and strip characters that can't) you set the `ascii` option to `yes`.

```YAML
rss:
  url: <url>
  ascii: yes
```

### Fix bad-formed XML

Sometimes feeds have non-escaped `&` in them. In correct XML every `&` whould be written as `&amp;` or inside `<![CDATA[]]>` block. If this problem is your case and maintainer of feed can't or don't want to fix it you can use `escape` option, that will try hard to fix unescaped `&`s in XML. 

This option is turned off by default because it's potentially CPU and memory intensive, also it makes process a bit slower.

**Example**:
```YAML
rss:
  url: https://url-here
  escape: yes
```