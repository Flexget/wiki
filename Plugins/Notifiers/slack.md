# *Slack*
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
|username|text|Override username
|icon_emoji|text|Override emoji icon


## Examples
<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

This example sends a Slack notification and overrides the default username and icon settings.

```yaml
notify:
  entries:
    via:
      - slack:
          web_hook_url: https://hooks.slack.com/services/XXXXXXXXX/YYYYYYYYY/ZZZZZZZZZZZZZZZZZZZZZZZZ
          username: Flexget
          icon_emoji: tv 
```