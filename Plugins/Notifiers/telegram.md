---
title: telegram
description: 
published: true
date: 2025-03-16T17:56:55.043Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:26:57.151Z
---

# [Notifiers](/Plugins/Notifiers) > Telegram
> Telegram is a part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-info}

Send a message to one or more Telegram users or groups upon accepting a download.


## Preparations

- Install the `Telegram` extra provided by FlexGet.
  ```bash
  uv tool install flexget[telegram]
  ```


- Create a bot & obtain a token for it (see https://core.telegram.org/bots#6-botfather).
- For direct messages (not to a group), start a conversation with the bot and click `START` in the Telegram app.
- For group messages, add the bot to the desired group and send a start message to the bot: `/start` (mind the
  leading `/`).

## Configuration

|Option|Type|Description|Default|
|---|---|---|---|
|bot_token|text|**Required.** Bot token.|N/A
|parse_mode|text|[Message parsing](https://core.telegram.org/bots/api#formatting-options). Can be `html`, `markdown` or `markdown_legacy`.|None
|disable_previews|boolean|Disable web page previews in messages.|False
|recipients|array|**At least one is required.** List of recipients type. Can be `chat_id`(recommended), `username`, `group` or `fullname`. See config example for details. Note: Values here are case-sensitive.|N/A
|socks_proxy|text|`socks5://user:pass@host:port` If no authentication is required, `user:pass` should be omitted, and you can omit the `@` at your discretion.|None
|images|array|Image paths, the specified images will be sent to Telegram.|None
  

In case of message error when using `parse_mode`, the parsing will fall back to basic. This can be caused due to unclosed tags (watch out for wandering underscore when using markdown)

`chat_id` can be obtained by asking [@raw_data_bot](https://t.me/raw_data_bot). The `chat_id` approach is the most recommended, because with this approach, you don't have to send a message to the bot to get the chat ID before the program runs. In addition, it is the most stable. Even if you change your name, the program will still work properly. `chat_id` can be a user's or a group's (including private groups). If the chat is a group, the chat id is negative. If it is a person, then positive.
Methods other than `chat_id` require sending a message just before the first run of the plugin (if you delete `db-config.sqlite` you will have to **do** this again). Note that Telegram does not allow robots to initiate conversations. With `chat_id` approach, you still need to have sent a message to the robot before (even if you delete "db-config.sqlite", you **do not** need to send a message again).
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
            bot_token: 5247092814:AAHmk7qdOMXEtZtGrnrzNxcoOazKNM51Atg
            parse_mode: markdown
            disable_previews: no
            recipients:
              - chat_id: 1694213419
              - username: my-user-name
              - group: my-group-name
              - fullname:
                  first: my-first-name
                  sur: my-sur-name
            socks_proxy: socks5://username:password@127.0.0.1:7897
            images:
              - 'image.png'
              - 'C:\Users\user\Pictures\image.jpg'
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
                - chat_id: '{? credentials.telegram.chat_id ?}'
```
