# [Notifiers](/Plugins/Notifiers) > Slack
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Slack can is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin allows Flexget to send notifications to a [Slack](https://www.slack.com/) channel or username via the [Incoming Webhooks](https://api.slack.com/incoming-webhooks) functionality.

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**web_hook_url**|URL|Web hook URL. **Required**
|channel|text|Override channel, use "@username" or "#channel"
|username|text|Override username|`Flexget`
|icon_emoji|text|Override emoji icon
|icon_url|URL|Image URL, will override notification icon
|attachments|array|Override message attachments

## Examples
<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

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
                    {% for key, value in imdb_actors.iteritems() %}
                      {{ value }}
                      {% if not loop.last %}, {% endif %}
                    {% endfor %}
                  short: false
```
