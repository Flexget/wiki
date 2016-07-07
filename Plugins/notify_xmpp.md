# Notify-XMPP
This plugin sends messages via XMPP, has been tested on Windows 7/64 so far, sending messages to Google Hangouts recipients.

The SleekXMPP library is required. To install it, run:

```
easy_install sleekxmpp
```

**Example:**

```
notify_xmpp:
      sender: from_jid@whatever.com
      password: mypassword
      recipients: to_jid@whatever.com
      title: 'New episode(s)!'
      text: '{{series_name}} {{tvdb_ep_id|default(series_id)}}{% if tvdb_ep_name|default(False) %}: {{tvdb_ep_name}}{% endif %}'
```

## Options

| **Name** | **Description** |
| --- | --- |
| sender | The sender jid |
| password | The sender password |
| recipient | One or more receipient JIDs to send the message to |
| title | [jinja2](/Plugins/set#DynamicFormatting) template used for notification title |
| text | [jinja2](/Plugins/set#DynamicFormatting) template used for notification body |

