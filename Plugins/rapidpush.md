= !RapidPush =
!RapidPush is an easy-to-use push notification service for Android devices.[[BR]]

You can receive notifications from FlexGet directly to your smartphone.[[BR]]

To use this Plugin you need the Android application "!RapidPush" which can be found within the [https://play.google.com/store/apps/details?id=com.syncoorp.rapidpush Google Play Store].[[BR]]
You need also an account at http://rapidpush.net .[[BR]]
After you have logged in to your account, goto your user interface and click on the tab "API-Keys". Then create a new or use an already existing one with this Plugin.

=== Configuration ===
{{{
rapidpush:
    apikey: xxxxxxx
    [category: category, default FlexGet]
    [title: title, default New release]
    [group: device group, default no group]
    [message: the message, to include the title from flexget insert {{title}} at the wanted position, default {{title}}]
    [priority: 0 - 6 (6 = highest), default 2 (normal)]
}}}

All options marked in `[]` are optional.

==== Example ====
{{{
rapidpush:
  priority: 3
  group: mydevices
  title: 'New Entries from: {{task}}'
  message: 'Downloaded: {{title}}'
  apikey: QwRJHc96BlbWZmCy1uBweVsGgikdzemDILTgoWUxlWyZkiUGeKsvwEDtGF9S0tr
}}}


If you do not provide a group, the notification is send to all your registered devices. If you want to filter out some devices you can create a group or setup a filter within our user interface.
If you decided to create a group, just provide the group name within the configuration.

