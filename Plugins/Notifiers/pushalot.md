# *Pushalot*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Pushalot is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>



This plugin provides the ability to send flexget notifications via the cross-platform notification system called [Pushalot](https://pushalot.com/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. Can also be a list. **Required**
|device|text|Target a specific device. Can also be a list|
|url|URL|Notification URL | Gets default from [notify](/Plugins/Notifiers/notify) plugin
|url_title|text|Text to be displayed as URL title 
|important|yes/no|Indicator whether the message should be visually marked as important within client app|`no`
|silent|yes/no|If set to True will prevent sending toast notifications to connected devices, resulting in silent delivery|`no`
|image|URL|Image thumbnail URL link
|source|text|Notification source name that will be displayed instead of authorization token's app name.|`FlexGet`
|timetolive|numeric|Time in minutes after which message automatically gets purged. Minimum is `0`, maxiumum is `43200`.

#### Example
```yaml
notify:
  entries:
    via:
      - pushalot:
          api_key: API_KEY
```

#### Advanced Example
```yaml
notify:
  entries:
    via:
      - pushalot: 
          api_key: 
            - api_key1
            - api_key2
          url: '{{ imdb_url }}'
          url_title: 'View {{ movie_name }} in IMDB'
          important: yes
          silent: no
          image: '{{ imdb_photo }}'
          source: test_source
          timetolive: 5
```

