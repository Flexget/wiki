# Notifier plugins

Notifications can be delivered by many different services. In order to allow any notification service to be used for any type of notification, we have split apart the plugins that generate messages from the plugins that deliver the messages. 

## Configuring your messages

The [notify](Plugins/notify) plugin is used to configure what notifications should be sent for a given task. In the future there may be other FlexGet subsystems which can also send notifications using these plugins.

## Notifiers
These plugins are responsible for delivering notifications. One or more of them can be chosen in the `via` section of the [notify](Plugins/notify) plugin.

| Plugin name | Description |
| --- | --- |
| [email](/Plugins/Notifiers/email) | Send an email message |
| [join](/Plugins/Notifiers/join) | Send a [Join](https://joaoapps.com/join/) notification |
| [toast](/Plugins/Notifiers/toast) | Popup a message on the computer running FlexGet. |
| [notifymyandroid](/Plugins/Notifiers/notifymyandroid) | Send a [NMA](http://www.notifymyandroid.com/) notification |
| [prowl](/Plugins/Notifiers/prowl) | Send a [Prowl](https://www.prowlapp.com/) notification |
| [pushalot](/Plugins/Notifiers/pushalot) | Send a [Pushalot](https://pushalot.com/) notification |
| [pushbullet](/Plugins/Notifiers/pushbullet) | Send a [Pushbullet](https://www.pushbullet.com/) notification |
| [pushover](/Plugins/Notifiers/pushover) | Send a [Pushover](https://pushover.net/apps/clone/Flexget) notification |
| [rapidpush](/Plugins/Notifiers/rapidpush) | Send a [Rapidpush](https://rapidpush.net/) notification |
| [slack](/Plugins/Notifiers/slack) | Send a [Slack](https://slack.com/) notification |
| [sms_ru](/Plugins/Notifiers/sms_ru) | Send a [SMS.RU](http://sms.ru/) notification |
| [telegram](/Plugins/Notifiers/telegram) | Send a [Telegram](https://telegram.org/) notification |
| [xmpp](/Plugins/Notifiers/xmpp) | Send an [XMPP](https://xmpp.org/) notification |

