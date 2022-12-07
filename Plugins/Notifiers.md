---
title: Notifiers
description: 
published: true
date: 2022-12-07T04:52:32.792Z
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

All available notifiers can be found from the plugins page [here](https://flexget.com/en/Plugins#notifier-services-output)