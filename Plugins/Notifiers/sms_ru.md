---
title: sms_ru
description: 
published: true
date: 2022-09-18T05:26:55.806Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:26:53.223Z
---

# [Notifiers](/Plugins/Notifiers) > SMS RU

> SMS RU can be is a part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-success}

This plugin provides the ability to send flexget notifications via the cross-platform notification system called [SMS RU](http://sms.ru/).

## Configuration

| Option |Type|  Description | Default |
| --- | ---| --- |---|
|**phone_number**|text|Phone number to SMS. **Required**
|**password**|text|Service password. **Required**

#### Example:
> Examples show a specifc scenario usage of the [notify](/Plugins/notify) plugin. See its wiki for a more detailed usage exaplantion.
{.is-warning}

```yaml
notify:
  entries:
    via:
      - sms_ru:
          phone_number: 6534563456345
          password: PASSWORD
```

