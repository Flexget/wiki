= Pushbullet =
== Overview ==
This plugin provides the ability to send flexget notifications via the Android notification system called [https://www.pushbullet.com/ Pushbullet].

> Pushbullet is a platform for sending and receiving push notifications.  On the server end, it provides an HTTP API for queueing messages to deliver to clients. On the client end, the Android clients receive those push notifications, show them to the user, and store them for offline viewing.  Due to the design of the systems, it does not store messages on the servers once they have been reliably received by the device client.

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