---
title: telegram
description: 
published: true
date: 2024-08-04T03:28:02.902Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:26:57.151Z
---

# [Notifiers](/Plugins/Notifiers) > Telegram
> Telegram is a part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-success}

Send a message to one or more Telegram users or groups upon accepting a download.


## Preparations

>Install `python-telegram-bot` python package
>```bash
>pip install python-telegram-bot==12.8
>```
{.is-info}

> Newer versions (13.0+) of python-telegram-bot are not compatible
{.is-danger}

* Create a bot & obtain a token for it (see https://core.telegram.org/bots#6-botfather).
* For direct messages (not to a group), start a conversation with the bot and click `START` in the Telegram app.
* For group messages, add the bot to the desired group and send a start message to the bot: `/start` (mind the
  leading `/`).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|bot_token|text|Bot token. **Required**
|parse_mode|text|[Message parsing](https://core.telegram.org/bots/api#formatting-options). Can be `html`, `markdown` or `markdown_legacy`. 
|disable_previews|boolean|Disable web page previews in messages. Optional (Default: `no`)
|recipients|text|List of recipients type. Can be `username`, `group` or `fullname`. See config example for details. **Note:** Values here are case-sensitive
|socks_proxy|text|Configuration for socks proxy to be used, must include `url` with URL to proxy, can include `username` and `password` for authentication. See config example below
  
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp; In case of message error when using `parse_mode`, the parsing will fall back to basic. This can be cause due to unclosed tags (watch out for wandering underscore when using markdown)
</div>
Not all Telegram users have a username. In such cases you would have to use the `fullname` approach. Otherwise, it is much easier to use the `username` configuration.

## Configuration examples
> Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
{.is-warning}

```yaml
my-task:
  notify:
    entries:
      message: Notification body.
      via:
        - telegram:
            bot_token: token
            parse_mode: markdown
            disable_previews: no
            recipients:
              - username: my-user-name
              - group: my-group-name
              - fullname:
                  first: my-first-name
                  sur: my-sur-name
            socks_proxy:
              url: http://127.0.0.1:3128
              username: username
              password: password
```

## Example using Jinja2 template and markdown
```yaml
templates:
  my_template_name:
    notify:
      entries:
        message: |+
          {%if task in ["retreive_from_couchpotato","dynamic_imdb_actors"]%}*New movie added to queue*
          {%else%}*Download Started from task:
          *{{task|replace("_", "-")}}
          {%endif%}
          {% if series_name is defined -%}
          *{{series_name}}* - {{series_id}} - {{quality|d('')}}
          *{{tvmaze_episode_name|d(tvdb_ep_name)|d('')}}*
          [Image]({{tvmaze_series_original_image|replace("_", "%5F")}})
          [Show page]({{tvmaze_series_url|replace("_", "%5F")}})
          {% elif imdb_name is defined -%}
          *{{imdb_name}}* - ({{imdb_year}})
          {{quality|d('')}}
          {{imdb_score}}/10 - {{imdb_votes}} votes
          {{imdb_genres|join(', ')|title}} 
          *Plot:* {{imdb_plot_outline}}
          [Image]({{tmdb_posters[0]|replace("_", "%5F")}})
          [Movie Page]({{imdb_url|d('')}})
          {% else -%}
          {{title}}
          {%- endif -%}
        via:
          - telegram:
              bot_token: '{? credentials.telegram.bot_token ?}'
              parse_mode: markdown_legacy
              recipients:
                - username: '{? credentials.telegram.username ?}'
```