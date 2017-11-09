# [Notifiers](/Plugins/Notifiers) > Microsoft Teams
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Microsoft Teams is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>

This plugin allows Flexget to send notifications to a [Microsoft Teams](https://products.office.com/en-us/microsoft-teams/group-chat-software) channel via the [Incoming Webhooks](https://msdn.microsoft.com/en-us/microsoft-teams/connectors) functionality.

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**web_hook_url**|URL|Web hook URL. **Required**
|title|text|Message title
|message|text|Message to be sent
|theme_color|text|Set message color



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
      - ms_teams:
          web_hook_url:  https://outlook.office.com/webhook/XXXXXXXXXXXXXXXXXZZZZZZZZZZZZZ
          title: Flexget
          message: Accepted title {{title}}
```