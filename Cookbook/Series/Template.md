# Manage series easier with a template
With [template](/Plugins/template) plugin you can avoid having to duplicate configuration in multiple tasks. This can be adapted for movies, comics etc. easily. See [template](/Plugins/template) documentation for more tips.

```
templates:
  tv:
    download: ~/torrents/series/
    exists_series: ~/storage/series/
    series:
      - pioneer one
      - south park

tasks:
  some feed:
    rss: http://example.com/
    template: tv

  another feed:
    rss: http://foobar.com/
    template: tv
```  

Uses plugins: [template](/Plugins/template), [RSS](/Plugins/rss), [series](/Plugins/series), [exists_series](/Plugins/exists_series), [download](/Plugins/download)

[Back to The Cookbook](/Cookbook)