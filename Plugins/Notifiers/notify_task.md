# *Notify task*

Use this plugin to send notification to one or more [notifer](/Plugins/Notifiers) plugins about the task.
This plugin runs on task exit and can be configured extensively

### Config:

| Options |Type|  Description | Default |
| --- | ---| --- |---|
|**to**|list|List of at least one notifer plugins, the same plugin can be used more than once. **Required**


You can also set any other attribute in the config, which will be passed to all configured notifiers. A default `title`, `message` and `url` are set.

The schema can also take any other property which will be passed to the configured notifier plugins.
<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp;
  All passed attributes support
  <a href="/Jinja/" class="alert-link">Jinja2 </a>
</div>

### Basic usage:
Looking at the schema, we can see that by default, using the minimal `notify_task` setting, a notifier will be defined as such:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    accept_all: yes
    download: /downloads/
    notify_task:
      to
        - pushover:
            user_key: user_key
```

Default data for `title`, `message` and `URL` will be used if no others were passed.

#### Advanced usage 1:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    regexp:
      accept_excluding:
        - bla
    download: /downloads/
    notify_task:
      to
        - pushover:
            user_key: user_key
            message: "Task {{ task_name }} is done!"
        - email:
           to: address@someone.com
      title: "Task {{ task_name }} has finished running"
```
In this example we use the global `title` to be passed to both `pushover` and `email`. The global `message` attribute is passed to `email` but `pushover` configured its `message internally, overriding the global value. 

<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp;
  Internal plugin attributes overide global ones
</div>

### Jinja2 usage
As can be viewed in the example, all attributes support Jinja2 usage. Soyou can render messages like this:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    regexp:
      accept_excluding:
        - bla
    download: /downloads/
    notify_task:
      to
        - pushover:
            user_key: user_key
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
      file_template: default
```
When using `file_template` it will render it and pass it as the `message` attribute.  
Some default file templates are supplied with flexget and are found under `/templates` dir in Flexget's run path. To use custom templates, simply create a `filename.template` file with the relevant data, and place it under `/templates` dir of the config path.  
As with all other attributes, `file_template` can be used globally or within a specfic notifer config.  
To view all available file templates use the [templates](/CLI/templates) command:  
```bash
flexget templates
```
### Using the same notifier more than once
There is no limitation to the number of times the same notifer can be used within a `notify_task` config:
```yaml
tasks:
  download_task:
    rss: http://stuff.com
    regexp:
      accept_excluding:
        - bla
    download: /downloads/
    notify_task:
      to
        - pushover:
            user_key: user_key1
        - pushover:
            user_key: user_key2
```
