# *Notify My Android*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Notify My Android can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>


This plugin provides the ability to send flexget notifications via the  notification system called [Notify My Android](http://www.notifymyandroid.com/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. **Required.**| 
|title|text|Notification title|Gets default from [notify](/Plugins/Notifiers/notify) plugin|
|application|text|Applicaiton name to display|`FlexGet`
|message|text| Notification message| Gets default from [notify](/Plugins/Notifiers/notify) plugin
|url|URL|Notification URL | Gets default from [notify](/Plugins/Notifiers/notify) plugin
|priority|numeric|Sets notification priority. Can be between -2 and 2.
|html|yes/no|Parse message as HTML
|developer_key|text|Optional developer key
| file_template | text|Name of the template file to use. See [notify](/Plugins/Notifiers/notify) plugin for more details| 


#### Example
```yaml
notifymyandroid:
  api_key: API_KEY
```

#### Advanced Example
```yaml
notifymyandroid:
  api_key: API_KEY
  application: Application name
  title: Downloading {{series_name}}
  message: |+
    <b>word</b> - display word in bold
    <i>word</i> - display word in italics
    <u>word</u> - display word underlined
    <font color="blue">word</font> - display word in blue text (most colors and   hex codes permitted)
    <a href="http://example.com/">word</a> - display word as a tappable link to http://example.com/
  priority: 2
  url: http://server.example.com/path/to/downloader/ui
  html: yes
```
