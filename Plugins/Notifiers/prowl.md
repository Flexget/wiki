---
title: prowl
description: 
published: true
date: 2022-09-18T05:26:28.266Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:26:25.614Z
---

# [Notifiers](/Plugins/Notifiers) > Prowl
> Prowl is part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-success}

Send messages to your iPhone using [Prowl](http://prowlapp.com).
## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|api_key|text|User's API Key. Can also be a list. **Required**
|url|URL|Notification URL | Gets default from [notify](/Plugins/Notifiers/notify) plugin
|application|text|The name of your application or the application generating the event|`FlexGet`
|provider_key|text|Optional	Your provider API key. Only necessary if you have been whitelisted
|priority|numeric| Set message priority. Values between -2 and 2 are accepted.| `0`|

### Example
Get your unique API key [here](/https://prowlapp.com/api_settings.php)

> Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
{.is-warning}

```yaml
notify:
  entries:
    via:
      - prowl:
          api_key: <your apikey>
```
