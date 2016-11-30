# Pushalot
## Overview
This plugin provides the ability to send FlexGet notifications via the cross-platform notification system called [Pushalot ](https://pushalot.com/).

> Pushalot is a platform for receiving custom push notifications to connected devices running Windows Phone or Windows 8. Custom means that those push notifications can be sent from virtually any source, as long as that source can interact with our open REST API.

## Configuration
### Simple
The simplest Pushalot plugin configuration **requires only the user token (`token`)**. This will broadcast the notification to the registered device/s associated with that token.
#### Example
```
pushalot:
  token: <token>
```

This will send the following message by default:
```
title: "Task <task name>"
body: "<series name> <series id> or <movie name> <movie year>" 
link: "<imdb url>
```
<img src="http://flexget.com/raw-attachment/wiki/Plugins/pushalot/pushlaot%20example.png">
### Advanced
More advanced configuration provides the ability to:
- Use several tokens <`token`> via a list. See example below for details.
- Set a title <`title`> (default is task name, Accepts Jinja2 tags) 
- Set a body <`body`> (default is mentioned above, Accepts Jinja2 tags) 
- Attach a URL <`link`> (default is '{{ imdb_url }}'', Accepts Jinja2 tags)
- Specify a URL name <`linktitle`> (default is none, Accepts Jinja2 tags)
- Specify priority <`important`> (accepts true/false, default is false)
- Specify sound mode <`silent`> (accepts true/false, default is false)
- Attach an image <`image`> (default is none, Accepts Jinja2 tags)
- Specify different app name <`source`> (default is "FlexGet")
- Specify message life span <`timetolive`> (accepts integer, value is minutes, default is none (never expires)

#### Example
```
pushalot: 
  token: 
    - token1
    - token2
  title: '{{ movie_name }}'
  body: '{{ imdb_plot_outline }}'
  link: '{{ imdb_url }}'
  linktitle: 'View {{ movie_name }} in IMDB'
  important: true
  silent: false
  image: '{{ imdb_photo }}'
  source: test_source
  timetolive: 5
```
### Attachments
* [Pushalot example notification on the windows 8 app](/attachments/Plugins/pushalot/pushlaot example.png)
* [72x72 FlexGet logo to use with Pushalot app](/attachments/Plugins/pushalot/flexget_logo.png)