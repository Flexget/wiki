= Pushalot =

== Overview ==
This plugin provides the ability to send flexget notifications via the cross-platform notification system called [https://pushalot.com/ Pushalot ].

> Pushalot is a platform for receiving custom push notifications to connected devices running Windows Phone or Windows 8. Custom means that those push notifications can be sent from virtually any source, as long as that source can interact with our open REST API.

== Configuration ==
=== Simple ===
The simplest Pushalot plugin configuration requires only the user token (`token). This will broadcast the notification to the registered device/s associated with that token.
==== Example ====
{{{
pushalot:
  token: <token>
}}}

This will send the following message by default:
{{{
title: <task name>
body:<series name>/<series id> or <movie name>\<movie year> 
}}}

=== Advanced ===
More advanced configuration provides the ability to:
- Use several tokens <'token'>
- Set a title <'title'> (default is task name, Accepts Jinja2 tags) 
- Set a body <'body'> (default is mentioned above, Accepts Jinja2 tags) 
- Attach a URL <'link'> (default is '{{ imdb_url }}'', Accepts Jinja2 tags)
- Specify a URL name <'linktitle'> (default is none, Accepts Jinja2 tags)
- Specify priority <'important'> (accepts true/false, default is false)
- Specify sound mode <'silent'> (accepts true/false, default is false)
- Attach an image <image> (default is none, Accepts Jinja2 tags)
- Specify different app name (default is "FlexGet")
- Specify message life span. (accepts integer, value is minutes, default is none (never expires)

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