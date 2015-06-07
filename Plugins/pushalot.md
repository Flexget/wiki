= Pushalot =

== Overview ==
This plugin provides the ability to send flexget notifications via the cross-platform notification system called [https://pushalot.com/ Pushalot ].

> Pushalot is a platform for receiving custom push notifications to connected devices running Windows Phone or Windows 8. Custom means that those push notifications can be sent from virtually any source, as long as that source can interact with our open REST API.

== Configuration ==
=== Simple ===
The simplest Pushalot plugin configuration requires only the user token (`token `). This will broadcast the notification to the registered device/s associated with that token.
==== Example ====
{{{
pushalot:
  token: <token>
}}}

=== Advanced ===
More advanced configuration provides the ability to:
* target a specific device (`device`)
* override the notification message title (`title`)
* override the notification message body (`message`)
* override the notification priority (`priority`)
* override the URL sent in the notification (`url`)
* override the default sound (`sound`)
* use multiple userkeys with a list for (`userkey`)

 device::
  (string) device name as specified in the Pushover configuration
 title::
  (string) accepts Jinja2 tags
 message::
  (string) accepts Jinja2 tags
 priority::
  (int) -1 = low, 0 = default, 1 = high
 url::
  (url) accepts Jinja2 tags

==== Example ====
{{{
pushover:
  userkey: 
    - o23ywmAaaxTYxn00jY2JAwQ2EeYXGt    
    - 0ydnaF3023jKadfkja9fjdkjaXfdfsaySGa
  apikey: nqC2fSOLCEyHHJcnusQtw4wqG2WbWf
  device: mobile
  title: Downloading {{series_name}}
  message: Episode {{series_id}}
  priority: 1
  url: http://server.example.com/path/to/downloader/ui
  sound: incoming
}}}