= !RapidPush =
!RapidPush is an easy-to-use push notification service for Android devices.[[BR]]

You can receive notifications from FlexGet directly to your smartphone.[[BR]]

To use this Plugin you need the Android application "!RapidPush" which can be found within the [https://play.google.com/store/apps/details?id=com.syncoorp.rapidpush Google Play Store].[[BR]]
You need also an account at http://rapidpush.net .[[BR]]
After you have logged in to your account, goto your user interface and click on the tab "API-Keys". Then create a new or use an already existing one with this Plugin.

You can now also use the channel feature, to send broadcast notifications to your subscribers.

=== Configuration ===
{{{
rapidpush:
    apikey: xxxxxxx (or a list of api keys)
    [category: category, default FlexGet]
    [title: title, default New release]
    [group: device group, default no group]
    [message: the message, to include the title from flexget insert {{title}} at the wanted position, default {{title}}]
    [channel: the broadcast notification channel, if provided it will be send to the channel subscribers instead of your devices, default no channel]
    [priority: 0 - 6 (6 = highest), default 2 (normal)]
    [notify_accepted: boolean true or false, default true]
    [notify_rejected: boolean true or false, default false]
    [notify_failed: boolean true or false, default false]
    [notify_undecided: boolean true or false, default false]
}}}

All options marked in `[]` are optional.

If you do not provide a group, the notification is send to all your registered devices. If you want to filter out some devices you can create a group or setup a filter within our user interface.
If you decided to create a group, just provide the group name within the configuration.

==== Example ====
{{{
rapidpush:
  priority: 3
  group: mydevices
  title: 'New Entries from: {{task}}'
  message: 'Downloaded: {{title}}'
  apikey: QwRJHc96BlbWZmCy1uBweVsGgikdzemDILTgoWUxlWyZkiUGeKsvwEDtGF9S0tr
}}}

==== Example with multiple API-Key ====
{{{
rapidpush:
  priority: 3
  group: mydevices
  title: 'New Entries from: {{task}}'
  message: 'Downloaded: {{title}}'
  apikey:
    - QwRJHc96BlbWZmCy1uBweVsGgikdzemDILTgoWUxlWyZkiUGeKsvwEDtGF9S0tr
    - 180b2042d270a23c902176ca582121ee180b2042d270a23c902176ca582121ee
}}}

==== Example to receive just rejected task entries ====
{{{
rapidpush:
  priority: 3
  group: mydevices
  title: 'New Entries from: {{task}}'
  message: 'Downloaded: {{title}}'
  apikey: QwRJHc96BlbWZmCy1uBweVsGgikdzemDILTgoWUxlWyZkiUGeKsvwEDtGF9S0tr
  notify_rejected: true
}}}

==== Example to receive rejected and failed task entries ====
{{{
rapidpush:
  priority: 3
  group: mydevices
  title: 'New Entries from: {{task}}'
  message: 'Downloaded: {{title}}'
  apikey: QwRJHc96BlbWZmCy1uBweVsGgikdzemDILTgoWUxlWyZkiUGeKsvwEDtGF9S0tr
  notify_rejected: true
  notify_failed: true
}}}

==== Example to receive ALL task entries (accepted, rejected, failed and undecided) ====
{{{
rapidpush:
  priority: 3
  group: mydevices
  title: 'New Entries from: {{task}}'
  message: 'Downloaded: {{title}}'
  apikey: QwRJHc96BlbWZmCy1uBweVsGgikdzemDILTgoWUxlWyZkiUGeKsvwEDtGF9S0tr
  notify_accepted: true
  notify_rejected: true
  notify_failed: true
  notify_undecided: true
}}}

==== Example to broadcast ====
{{{
rapidpush:
  channel: MY_CHANNEL
  title: 'New Entries from: {{task}}'
  message: 'News: {{title}}'
  apikey: QwRJHc96BlbWZmCy1uBweVsGgikdzemDILTgoWUxlWyZkiUGeKsvwEDtGF9S0tr
}}}