---
title: Notifiers
description: 
published: true
date: 2022-12-07T05:00:06.532Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:01:16.981Z
---

# Notifier plugins

Notifications can be delivered by many different services. In order to allow any notification service to be used for any type of notification, we have split apart the plugins that generate messages from the plugins that deliver the messages. 

## Configuring your messages

The [notify](/Plugins/notify) plugin is used to configure what notifications should be sent for a given task. In the future there may be other FlexGet subsystems which can also send notifications using these plugins.

## Notifiers
These plugins are responsible for delivering notifications. One or more of them can be chosen in the `via` configuration option of the [notify](/Plugins/notify) plugin.

| **Keyword** | **Description** |
| --- | --- |
| [email](/Plugins/Notifiers/email) | Send an email message |
| [gotify](/Plugins/Notifiers/gotify) | Send a [Gotify](https://gotify.net) notification |
| [join](/Plugins/Notifiers/join) | Send a [Join](https://joaoapps.com/join/) notification |
| [notifymyandroid](/Plugins/Notifiers/notifymyandroid) | Send a [NMA](http://www.notifymyandroid.com/) notification |
| [mqtt](/Plugins/Notifiers/mqtt) | Send MQTT notification |
| [matrix](/Plugins/Notifiers/matrix) | Send [matrix](https://matrix.org) notification |
| [prowl](/Plugins/Notifiers/prowl) | Send a [Prowl](https://www.prowlapp.com/) notification |
| [pushalot](/Plugins/Notifiers/pushalot) | Send a [Pushalot](https://pushalot.com/) notification |
| [pushbullet](/Plugins/Notifiers/pushbullet) | Send a [Pushbullet](https://www.pushbullet.com/) notification |
| [pushover](/Plugins/Notifiers/pushover) | Send a [Pushover](https://pushover.net/apps/clone/Flexget) notification |
| [pushsafer](/Plugins/Notifiers/pushsafer) | Send a [Pushsafer](https://www.pushsafer.com/en/FlexGet) notification |
| [rapidpush](/Plugins/Notifiers/rapidpush) | Send a [Rapidpush](https://rapidpush.net/) notification |
|[discord](/Plugins/Notifiers/discord) | Send a [Discord](https://discordapp.com/) notification
| [slack](/Plugins/Notifiers/slack) | Send a [Slack](https://slack.com/) notification |
| [sms_ru](/Plugins/Notifiers/sms_ru) | Send a [SMS.RU](http://sms.ru/) notification |
| [telegram](/Plugins/Notifiers/telegram) | Send a [Telegram](https://telegram.org/) notification |
| [xmpp](/Plugins/Notifiers/xmpp) | Send an [XMPP](https://xmpp.org/) notification |
| [ms_teams](/Plugins/Notifiers/ms_teams) |Send a [Microsoft Teams](https://products.office.com/en-us/microsoft-teams/group-chat-software) notification |
