# Series name as a category
When using [sabnzbd](/Plugins/sabnzbd) you can use series name as a category by utilizing [set](/Plugins/set) plugin. The category name will be exactly the one written in as a series name.

```
tasks:
  my-feed:
    .
    .
    series:
      settings:
        720p:
          set:
            category: '{{series_name}}'
      720p:
        - chuck
        - south park
    sabnzbd:
      key: 1234567890
      url: http://127.0.0.1:8080/sabnzbd/api?
```

[Back to The Cookbook](/Cookbook)