# Download Heroes comics
Download all/new heroes comics from [nbc.com](http://nbc.com/Heroes). This uses advanced text-parsing plugin and does not represent accurately average usage.

```
feeds:
  heroes:
    interval: 6 hours
    text:
      url: http://www.nbc.com/Heroes/js/novels.js
      entry:
        title: novelTitle = "(.*)"
        url: novelPrint = "(.*)"
      format:
        url: http://www.nbc.com%(url)s
    download: ~/heroes/
```

Uses plugins: [interval](/Plugins/interval), [text](/Plugins/text), [download](/Plugins/download)

[Back to The Cookbook](/Cookbook)