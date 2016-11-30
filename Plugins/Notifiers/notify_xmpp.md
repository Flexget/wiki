# *XMPP*
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; XMPP can be used as a part of [notifier](/Plugins/Notifiers) plugin system.
</div>
This plugin sends messages via XMPP, has been tested on Windows 7/64 so far, sending messages to Google Hangouts recipients.

The SleekXMPP library is required. To install it, run:

```
pip install sleekxmpp
```
## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|sender|email|Sender's JID. **Required**
|password|text|Sender's password. **Required**
|recipients|email|Recipients JID. Can also be a list. **Required**
|title|text|Notification title|Gets default from [notify](/Plugins/Notifiers/notify) plugin|
|message|text| Notification message| Gets default from
| file_template | text|Name of the template file to use. See [notify](/Plugins/Notifiers/notify) plugin for more details| 
**Example:**

```yaml
xmpp:
  sender: from_jid@whatever.com
  password: mypassword
  recipients: to_jid@whatever.com
  title: 'New episode(s)!'
  message: '{{series_name}} {{tvdb_ep_id|default(series_id)}}{% if tvdb_ep_name|default(False) %}: {{tvdb_ep_name}}{% endif %}'
```


