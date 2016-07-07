# Notify-OSD
**`Requirement:`**
Must have a notification system like dbus for linux operating systems. Has been tested on Ubuntu 12.04 only!

**Syntax:**

```
notify_osd: [yes](/yes)
  title_template: [Supports jinja2 templating. Default: {{task.name}}]
  item_template:  [Supports jinja2 templating. Default: {{title}}]
```

## Options
All options are optional. Please see [jinja2](/Plugins/set#DynamicFormatting) for more formatting options.

```
notify_osd: yes
```

  


| **Name** | **Description** |
| --- | --- |
| title_template | [jinja2](/Plugins/set#DynamicFormatting) template used for notification title |
| item_template | [jinja2](/Plugins/set#DynamicFormatting) template used for notification body |


## Linux Users
Please ensure you have a notification system on your distribution before enabling this option.

## Windows Users
**DO NOT ENABLE THIS OPTION**