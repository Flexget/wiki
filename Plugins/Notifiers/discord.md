---
title: discord
description: 
published: true
date: 2022-09-18T05:25:37.311Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:25:34.649Z
---

# [Notifiers](/Plugins/Notifiers) > Discord
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Discord is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin is used to send notification to a discord server using the [webhook](https://discordapp.com/developers/docs/resources/webhook#execute-webhook) functionnality.

## Configuration

|Option |Type |Description| Default |
| --- | ---| --- |---|
|web_hook_url | url | Server webhook url. **Required**|
|username| text |override the default username of the webhook|`Flexget`
|avatar_url|url|override the default avatar of the webhook
|embeds|array|[embeded](https://discordapp.com/developers/docs/resources/channel#embed-object) content

## Examples
<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

The following configuration send a webhook message to a discord server containing embeds object. Refer to [Embed object documentation](https://discordapp.com/developers/docs/resources/channel#embed-object) for more information on how to use them.
```yaml
    notify:
      entries:
        message: "{{series_name}} - {{series_id }}"
        via:
          - discord:
              web_hook_url: https://discordapp.com/api/webhooks/XXXXXXXXXXX/YYYYYYYYYY
              avatar_url: https://avatars2.githubusercontent.com/u/17483320?s=400&v=4
              username: "Flexget"
              embeds:
                - title: "{{series_name}}"
                  description: "{{tvmaze_series_summary|default('Unknown')}}"
                  url: "{{tvmaze_series_url}}"
                  color: 0xe67e22
                  author:
                    name: "Flexget"
                    url: "https://flexget.com"
                    icon_url: "https://i.imgur.com/R66g1Pe.jpg"
                  fields:
                    - name: "Episode Name:"
                      value: "{{tvmaze_episode_name|default('Unknown')}}"
                      inline: True
                    - name: "Score"
                      value: "{{tvmaze_series_rating|default('Unknown')}}"
                      inline: True
                    - name: "Made in"
                      value: ":flag_jp:"
                  thumbnail:
                    url: "{{tvdb_ep_image|default('https://i.imgflip.com/j69nf.jpg')}}"
                  image:
                    url: "{{tvmaze_series_original_image}}"
```
