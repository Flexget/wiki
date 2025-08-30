---
title: slack
description: 
published: true
date: 2025-08-30T07:37:39.350Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:26:49.250Z
---

# [Notifiers](/Plugins/Notifiers) > Slack
> Slack can is a part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-success}

This plugin allows Flexget to send notifications to a [Slack](https://www.slack.com/) channel or username via the [Incoming Webhooks](https://api.slack.com/incoming-webhooks) functionality.

## Configuration

### Block Kit

| Option |Type|  Description | Required
| --- | ---| --- |---|
|**web_hook_url**|URL|Web hook URL|✅|
|blocks|array|see example below|❌|

### Legacy

| Option |Type|  Description | Default | Required|
| --- | ---| --- |---|---|
|**web_hook_url**|URL|Web hook URL||✅|
|channel|text|Override channel, use "@username" or "#channel"||❌|
|username|text|Override username|`Flexget`|❌|
|icon_emoji|text|Override emoji icon||❌|
|icon_url|URL|Image URL, will override notification icon||❌|
|attachments|array|Override message attachments||❌|

## Examples

### Block Kit

#### Config

```yaml
tasks:
  slack:
    mock:
      - { ... }
    accept_all: yes
    notify:
      entries:
        via:
          - slack:
              web_hook_url: "https://hooks.slack.com/services/T0F1*****/B099*******/OOPTXTzIJfMyaHWG********"
              blocks:
                - section:
                    text: '<{{ tvdb_url }}|{{ series_name }} ({{ series_id }})>'
                - section:
                    text: '{{ tvdb_ep_overview }}'
                    image:
                      url: "https://api.slack.com/img/blocks/bkb_template_images/plants.png"
                      alt_text: 'plants'
                    fields:
                      - '*Score*'
                      - '*Genres*'
                      - '{{ imdb_score }}'
                      - "{{ imdb_genres | join(', ') | title }}"
                      - '*Rating*'
                      - '*Cast*'
                      - '{{ imdb_mpaa_rating }}'
                      - >
                        {% for key, value in imdb_actors.items() %}{{ value }}{% if not loop.last %}, {% endif %}
                        {% endfor %}
                - image:
                    url: "{{ tvdb_banner }}"
                    alt_text: "{{ series_name }} Banner"
                - divider: True
                - context:
                    - image:
                        url: 'https://image.freepik.com/free-photo/red-drawing-pin_1156-445.jpg'
                        alt_text: 'red pin'
                    - text: ':round_pushpin:'
                    - text: 'Task: {{ task }}'
```

#### Example output
![image](https://user-images.githubusercontent.com/249456/74075454-4b5e1d00-49c7-11ea-9e58-438a90942812.png)

#### Useful resources
[Sending messages using incoming webhooks](https://api.slack.com/messaging/webhooks)

### Legacy

The following example sends a Slack message along with an attachment for more context. Refer to the [message attachment docs](https://api.slack.com/docs/message-attachments) for all available parameters.

```yaml
notify:
  entries:
    via:
      - slack:
          web_hook_url: https://hooks.slack.com/services/XXXXXXXXX/YYYYYYYYY/ZZZZZZZZZZZZZZZZZZZZZZZZ
          message: "{{ imdb_name }}"
          icon_emoji: movie_camera
          attachments:
            - title: "{{ imdb_name }} ({{ imdb_year }})"
              image_url: "{{ tmdb_posters | first }}" # better quality
              title_link: "{{ imdb_url }}"
              fallback: "{{ imdb_name }} ({{ imdb_year }})"
              text: "{{ imdb_plot_outline }}"
              color: "#e67e22"
              footer: "{{ task }}"
              footer_icon: "https://avatars2.githubusercontent.com/u/17483320?s=400&v=4"
              fields:
                - title: Runtime
                  value: "{{ tmdb_runtime }} mins"
                  short: true
                - title: Score
                  value: "{{ imdb_score }}"
                  short: true
                - title: Genres
                  value: "{{ imdb_genres | join(', ') | title }}"
                  short: true
                - title: Rating
                  value: "{{ imdb_mpaa_rating }}"
                  short: true
                - title: Cast
                  value: >
                    {% for key, value in imdb_actors.items() %}
                      {{ value }}
                      {% if not loop.last %}, {% endif %}
                    {% endfor %}
                  short: false
```
#### Useful resources
[Legacy custom integrations incoming webhooks](https://api.slack.com/legacy/custom-integrations/messaging/webhooks)