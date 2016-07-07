# Manual
Any tasks that have this plugin enabled will not be run unless they are explicitly called with the [--task](/Plugins/--task) plugin.

**Example:**
```
tasks:
  thetask:
    manual: yes
```
FlexGet will not execute `thetask` unless you run it with the command `flexget execute --task thetask`