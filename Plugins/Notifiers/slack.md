# *Slack*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Slack can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin allows Flexget to send notifications to a [Slack](https://www.slack.com/) channel or username via the [Incoming Webhooks](https://api.slack.com/incoming-webhooks) functionality.

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**web_hook_url**|URL|Web hook URL. **Required**
|channel|text|Override channel, use "@username" or "#channel"
|username|text|Override username
|icon_emoji|text|Override emoji icon
|message|text| Notification message| Gets default from [notify](/Plugins/Notifiers/notify) plugin
| file_template | text|Name of the template file to use. See [notify](/Plugins/Notifiers/notify) plugin for more details|


## Example
This example sends a Slack notification and overrides the default username and icon settings.

```
slack:
  web_hook_url: https://hooks.slack.com/services/XXXXXXXXX/YYYYYYYYY/ZZZZZZZZZZZZZZZZZZZZZZZZ
  username: Flexget
  icon_emoji: tv 
```