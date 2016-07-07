# Slack
## Overview
This plugin allows Flexget to send notifications to a [Slack](https://www.slack.com/) channel or username via the [Incoming Webhooks](https://api.slack.com/incoming-webhooks) functionality.

## Configuration Options
The only required configuration option is the Incoming Webhook URL. To use this plugin, add an Incoming Webhook for your Slack team and then copy and paste the entire URL into the Flexget config file. Optionally you can override the default text, channel, username, or icon_emoji settings.

```
slack:
  webhook-url: <string>
  [text: <string>] (default: "{{task}} - Download started:
                              {% if series_name is defined %}
                              {{tvdb_series_name|d(series_name)}} {{series_id}} {{tvdb_ep_name|d('')}}
                              {% elif imdb_name is defined %}
                              {{imdb_name}} {{imdb_year}}
                              {% else %}
                              {{title}}
                              {% endif %}"
  [channel: <string>] (override channel, use "@username" or "#channel")
  [username: <string>] (override username)
  [icon-emoji: <string>] (override emoji icon, do not include the colons:
                          e.g., use "tv" instead of ":tv:")
```


## Example
This example sends a Slack notification and overrides the default username and icon settings.

```
slack:
  webhook-url: https://hooks.slack.com/services/XXXXXXXXX/YYYYYYYYY/ZZZZZZZZZZZZZZZZZZZZZZZZ
  username: Flexget
  icon-emoji: tv 
```