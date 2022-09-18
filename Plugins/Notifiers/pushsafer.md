---
title: pushsafer
description: 
published: true
date: 2022-09-18T05:26:44.006Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:26:41.361Z
---

# [Notifiers](/Plugins/Notifiers) > Pushsafer
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Pushsafer is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>



This plugin provides the ability to send flexget notifications via the cross-platform notification system called [Pushsafer](https://www.pushsafer.com/en/FlexGet).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **private_key**| text| Pushsafer's private or alias key. **Required.**
|device|text|Target a specific device or device group id.|blank
|url|URL|Notification URL|blank
|url_title|text|Text to be displayed as URL title|blank
|sound|numeric|Override default notifcation sound. Must one of [Pushsafer's supported sounds](https://www.pushsafer.com/en/pushapi)|blank
|icon|numeric|Override default notifcation icon. Must one of [Pushsafer's supported icons](https://www.pushsafer.com/en/pushapi)|1 or blank
|vibration|numeric|How often the device should vibrate (0-3)|0
|time2live|numeric|Time in minutes, after which message automatically gets purged (0-43200)|0 or blank

### Examples

Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.

#### Simple notification for each accepted entry
The simplest Pushsafer plugin configuration requires only the private key (`private_key`). This will broadcast the notification to all registered devices.

```yaml
notify:
  entries:
    via:
      - pushsafer:
          private_key: PRIVATE_KEY
```

#### More advanced version
```yaml
notify:
  entries:
    via:
      - pushsafer:
          private_key: o23ywmAaaxTYxn00jY2JAwQ2EeYXGt    
          device: 119
          url: http://server.example.com/path/to/downloader/ui
          sound: 12
          icon: 20
          sound: 8
          vibration: 1
```

#### Example with Jinja2 tags
```yaml
notify:
  entries:
    title: >
      {%if task in ["task_a","task_b"](/"task_a","task_b")%} New movie added to queue
      {%else%}Download Started from task {{task}}
      {%endif%}
    message: >
      {% if series_name is defined %}{{series_name}} - {{series_id}} - {{trakt_ep_name}} - {{quality|d('')}}
      {% elif imdb_name is defined%}{{movie_name}} - {{quality}}
      {% else %}{{title}}
      {% endif %}
    via:
      - pushsafer:
          private_key: '{? credentials.pushsafer.private_key ?}'
          sound: 8
          icon: 20
          vibration: 1
          url: '{{trakt_series_trakt_url|d(imdb_url)}}'
          url_title: Link
```
#### Example with HTML tags
```yaml
notify:
  entries:
    via:
      - pushsafer:
          private_key: '{? credentials.pushsafer.private_key ?}'
    message: |+
      [b]word[/b] - display word in bold
      [i]word[/i] - display word in italics
      [u]word[/u] - display word underlined
      [color=#FF0000>word[/color] - display word in red text (most colors and hex codes permitted)
      [url=https://www.pushsafer.com]Pushsafer[/url] - display word as a tappable link to https://www.pushsafer.com/
```
