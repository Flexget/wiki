# Simple Ebook Recipes
# Using download plugin
This recipe uses the regexp plugin to download torrents from an rss feed to a specified path.

```
tasks:
  books:
    rss: http://example.com
    regexp:
      accept:
        - Some Publisher
        - Some Magazine
    download: /path/to/torrents/
```

Uses plugins:  [regexp](/Plugins/regexp),[download](/Plugins/download)