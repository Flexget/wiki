---
title: xmpp
description: 
published: true
date: 2022-09-18T05:27:07.779Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:27:05.215Z
---

# [Notifiers](/Plugins/Notifiers) > XMPP
> XMPP is a part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-success}
This plugin sends messages via XMPP, has been tested on Windows 7/64 so far, sending messages to Google Hangouts recipients.

## Preparations

[Includes/PluginRequiresPip](/Includes/PluginRequiresPip){.include}

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**sender**|email|Sender's JID. **Required**
|**password**|text|Sender's password. **Required**
|**recipients**|email|Recipients JID. Can also be a list. **Required**

> Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
{.is-warning}

```yaml
notify:
  entries:
    via:
      - xmpp:
          sender: from_jid@whatever.com
          password: mypassword
          recipients: to_jid@whatever.com
```


