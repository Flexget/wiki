= Notify-OSD =

'''{{{Requirement:}}}'''
Must have a notification system like dbus for linux operating systems. Has been tested on Ubuntu 12.04 only!

'''Example:'''

{{{
notify_osd: [yes]
  title_template: [Supports jinja2 templating. Default: {{task.name}}]
  item_template:  [Supports jinja2 templating. Default: {{title}}]
}}}

== Options ==

All options are optional. Please see [wiki:Plugins/set#DynamicFormatting jinja2] for more formatting options.

{{{
notify_osd: yes
}}}

||'''Name'''||'''Description'''||
||title_template||[wiki:Plugins/set#DynamicFormatting jinja2] template used for notification title||
||item_template||[wiki:Plugins/set#DynamicFormatting jinja2] template used for notification body||


== Linux Users ==

Please ensure you have a notification system on your distribution before enabling this option.

== Windows Users ==

'''DO NOT ENABLE THIS OPTION'''