= Pushbullet =
== Overview ==
This plugin provides the ability to send flexget notifications via the Android notification system called [https://www.pushbullet.com/ Pushbullet].

> Pushbullet shows you all of your phone's notifications right on your computer so you never miss a notification again!
> Pushbullet also lets you send push notifications to yourself and to your friends!
> Why send push notifications with Pushbullet? Because it's the easiest and fastest way to send almost anything to your phone or to your friends.
> What can you push with Pushbullet? Send links, pictures, files, lists, notes, and more right into your phone's notification tray, to your computer, or to a friend, really fast.

== Configuration ==
{{{
pushbullet:
    apikey: <API_KEY>
    device: <DEVICE_IDEN>
    [title: <MESSAGE_TITLE>] (default: "{{task}} - Download started" -- accepts Jinja2)
    [body: <MESSAGE_BODY>] (default: "{{series_name}} {{series_id}}" -- accepts Jinja2)
}}}

DEVICE_IDEN can by found by running: 
{{{
curl -u <API_KEY>: https://api.pushbullet.com/api/devices
}}}