---
import:
 - Includes/PluginRequiresPip
packages: sleekxmpp
---
# [Notifiers](/Plugins/Notifiers) > XMPP
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; XMPP is a part of the [notifier](/Plugins/Notifiers) plugin system.
</div>
This plugin sends messages via XMPP, has been tested on Windows 7/64 so far, sending messages to Google Hangouts recipients.

## Preparations

{{> Includes/PluginRequiresPip }}

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**sender**|email|Sender's JID. **Required**
|**password**|text|Sender's password. **Required**
|**recipients**|email|Recipients JID. Can also be a list. **Required**

<div class="alert alert-warning" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
</div>

```yaml
notify:
  entries:
    via:
      - xmpp:
          sender: from_jid@whatever.com
          password: mypassword
          recipients: to_jid@whatever.com
```


