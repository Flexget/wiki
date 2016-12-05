# Notify

Use this plugin to send notification to one or more [notifer](/Plugins/Notifiers) plugins.
This plugin runs on task exit and can be configured extensively

### Config:

| Options |Type|  Description | Default |
| --- | ---| --- |---|
|**to**|list|List of at least one notifer plugins, the same plugin can be used more than once. **Required**
|scope|text|Can be `task` or `entries`. Defines the scope of the data to be used in the notification|`entries`
|what|text| One or more of `entries`, `accepted`, `rejected`, `failed` or `undecided`. The data to iterate on. Relevant only when `scope` is set to `entries`.|`accepted`

You can also set any other attribute in the config, which will be passed to all configured notifiers. A default `title`, `message` and `url` are set depending on the selected scope.

The schema can also take any other property which will be passed to the configured notifier plugins.
<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp;
  All passed attributes support Jinja2 usage
</div>

### Basic usage:
Looking at the schema, we can see that by default, using the minimal `notify` setting, a notifier will be defined as such:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    accept_all: yes
    download: /downloads/
    notify:
      to
        - pushover:
            user_key: user_key
```
This will use `entries` scope and send a notification for each `accepted` one. It is functionally similar to direcly calling the notifier as such:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    accept_all: yes
    download: /downloads/
    pushover:
      user_key: user_key
```
Each scope has default data for `title`, `message` and `URL` which will be used if no others were passed.
#### Advanced usage 1:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    regexp:
      accept_excluding:
        - bla
    download: /downloads/
    notify:
      to
        - pushover:
            user_key: user_key
        - email:
           to: address@someone.com
      what: rejected
      title: "Rejected entries in task {{ task_name }}"
      message: "Entry {{ title }} was rejected due to {{ reason }}"
```
This will trigger a notification for both `pushover` and `email` for each rejected entry.
#### Advanced usage 2:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    regexp:
      accept_excluding:
        - bla
    download: /downloads/
    notify:
      to
        - pushover:
            user_key: user_key
            message: "Task {{ task_name }} is done!"
        - email:
           to: address@someone.com
      scope: task
      title: "Task {{ task_name }} has finished running"
```
In this example we use the global `title` to be passed to both `pushover` and `email`. The global `message` attribute is passed to `email` but `pushover` configured its `message internally, overriding the global value. 

<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp;
  Internal plugin attributes overide global ones
</div>

### Jinja2 usage
As can be viewed in the example, all attributes support Jinja2 usage. So if scope is set to `entries`, you can render messages like this:
```yaml
tasks:
  download_stuff:
    rss: http://stuff.com
    accept_all: yes
    imdb_lookup: yes
    tmdb_lookup: yes
    tvmaze_lookup: yes
    notify:
      to:
      - telegram:
          bot_token: '{{secrets.credentials.telegram.bot_token}}'
          parse_mode: markdown
          recipients:
            - username: '{{secrets.credentials.telegram.username}}'
          message: |+
            {%if task in ["retreive_from_couchpotato","dynamic_imdb_actors"]%}*New movie added to list*
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
```
If scope is set to `task`, different attributes can be used:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    regexp:
      accept_excluding:
        - bla
    download: /downloads/
    notify:
      to
        - pushover:
            user_key: user_key
      scope: task
      message: |+
        {% if task.aborted -%}
        Task {{task_name}} was aborted because: {{task.abort_reason}}
        {% endif -%}
        {% if task.accepted -%}
        {%- for group in task.accepted|groupby('task') %}
        FlexGet has just downloaded {{group.list|length}} new entries for task {{group.grouper}}:
          {%- for entry in group.list %}
        - {{entry.title}} ({{entry.url}}){% if entry.output|d(false) %} => {{entry.output}}{% endif %}
          {% endfor %}
        {% endfor %}
        {% endif -%}
        {% if task.failed -%}
        {%- for group in task.failed|groupby('task') %}
        The following entries have failed for task {{group.grouper}}:
          {%- for entry in group.list %}
            - {{entry.title}} ({{entry.url}}) Reason: {{entry.reason|d('unknown')}}
          {% endfor %}
        {% endfor %}
        {% endif %}
```
While these advanced templates can be very useful, they can appear bery bulky in the config. Instead you could use the `file_template` attribute:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    regexp:
      accept_excluding:
        - bla
    download: /downloads/
    notify:
      to
        - pushover:
            user_key: user_key
      scope: task
      file_template: default_task
```
When using `file_template` it will render it and pass it as the `message` attribute.  
Some default file templates are supplied with flexget and are found under `/templates` dir in Flexget's run path. To use custom templates, simply create a `filename.template` file with the relevant data, and place it under `/templates` dir of the config path.  
As with all other attributes, `file_template` can be used globally or within a specfic notifer config.
### Using the same notifier more than once
There is no limitation to the number of times the same notifer can be used within a `notify` config:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    regexp:
      accept_excluding:
        - bla
    download: /downloads/
    notify:
      to
        - pushover:
            user_key: user_key1
        - pushover:
            user_key: user_key2
```
