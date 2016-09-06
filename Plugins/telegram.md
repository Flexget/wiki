# Telegram
Send a message to one or more Telegram users or groups upon accepting a download.


## Preparations
* Install 'python-telegram-bot' python pkg (i.e. `pip install python-telegram-bot`)
* Create a bot & obtain a token for it (see https://core.telegram.org/bots#botfather).
* For direct messages (not to a group), start a conversation with the bot and click "START" in the Telegram app.
* For group messages, add the bot to the desired group and send a start message to the bot: "/start" (mind the
  leading '/').


## Configuration example
```
my-task:
  telegram:
    bot_token: token
    template: {{title}}
    parse_mode: markdown
    recipients:
      - username: my-user-name
      - group: my-group-name
      - fullname:
          first: my-first-name
          sur: my-sur-name
```

## Example using Jinja2 template and markdown
```
telegram:
  telegram:
    bot_token: '{{secrets.credentials.telegram.bot_token}}'
    parse_mode: markdown
    recipients:
      - username: '{{secrets.credentials.telegram.username}}'
    template: |+
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
      [Image]({{tmdb_posters[0](/0)|replace("_", "%5F")}})
      [Movie Page]({{imdb_url|d('')}})
      {% else -%}
      {{title}}
      {%- endif -%}
```

## Configuration notes
You may use any combination of recipients types (`username`, `group` or `fullname`) - 0 or more of each (but you
need at least one total...).


## `template`
Optional. The template from the example is the default.

## `parse_mode`
Optional. Whether the template uses `markdown` or `html` formatting. 

NOTE: The markdown parser fall back to basic parsing if there is a parsing error. This can be cause due to unclosed tags (watch out for wandering underscore when using markdown)

## `username` vs. `fullname`
Not all Telegram users have a username. In such cases you would have to use the `fullname` approach. Otherwise, it
is much easier to use the `username` configuration.
