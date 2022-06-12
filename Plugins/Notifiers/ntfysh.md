# [Notifiers](/Plugins/Notifiers) > ntfy.sh
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; ntfy.sh is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin provides the ability to send flexget notifications via the cross-platform notification system called ntfy.sh.

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**topic**|text|Specify the topic to publish to. **Required**|
| url| URL| ntfy.sh server. Can be set for selfhosted server.|`ntfy.sh`
|priority|integer| Set priority of notification.|`3`
|delay|text| Delay in seconds before sending notification
|tags|text| Comma separated list of tags to add to message
|username|text| Username if authentication is required
|password|text| Password if authentication is required

#### Examples
<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

```yaml
notify:
  entries:
    via:
      - ntfysh:
          topic: "topic"
```

#### Advanced Example
```yaml
notify:
  entries:
    via:
      - ntfysh: 
          topic: "topic"
          url: "https://ntfy.domain.com"
          priority: 5
          delay: 30s
          tags: tag1,tag2
          username: "ntfy_user"
          password: "ntfy_password"
```
