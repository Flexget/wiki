---
title: pushbullet
description: 
published: true
date: 2022-09-18T05:26:36.119Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:26:33.564Z
---

# [Notifiers](/Plugins/Notifiers) > Pushbullet
> Pushbullet is a part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-success}

This plugin provides the ability to send flexget notifications via the cross-platform notification system called [Pushbullet](https://www.pushbullet.com/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
| **api_key**| text| User's API key. **Required**|
|device|text|Target a specific device. Can also be a list. 
|email|email|Target user's emails. Can also be a list. 
|channel|text|Target channel. Can also be a list. 
|url|URL|Notification URL | 

> Only one of `email`, `device` or `channel` can be used per config
{.is-info}

### Examples


### Send notification for each accepted entry
```yaml
notify:
  entries:
    via:
      - pushbullet:
          api_key: API_key
```


