---
title: notifymyandroid
description: 
published: true
date: 2022-09-18T05:26:20.407Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:26:17.705Z
---

# [Notifiers](/Plugins/Notifiers) > Notify My Android
> Notify My Android can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
{.is-success}


Now defunct May 2018 - This plugin provides the ability to send flexget notifications via the  notification system called [Notify My Android](http://www.notifymyandroid.com/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. **Required.**| 
|application|text|Applicaiton name to display|`FlexGet`
|url|URL|Notification URL | Gets default from [notify](/Plugins/Notifiers/notify) plugin
|priority|numeric|Sets notification priority. Can be between -2 and 2.
|html|yes/no|Parse message as HTML
|developer_key|text|Optional developer key


#### Examples
> Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
{.is-warning}

```yaml
notify:
  entries:
    via:
      - notifymyandroid:
          api_key: API_KEY
```

#### Advanced Example
```yaml
notify:
  entries:
    via:
      - notifymyandroid:
          api_key: API_KEY
          application: Application name
          priority: 2
          url: http://server.example.com/path/to/downloader/ui
          html: yes
```
