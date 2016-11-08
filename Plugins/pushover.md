# Pushover
## Overview
This plugin provides the ability to send flexget notifications via the cross-platform notification system called [Pushover](https://pushover.net/apps/clone/Flexget).

> Pushover is a platform for sending and receiving push notifications.  On the server end, it provides an HTTP API for queueing messages to deliver to clients. On the client end, the iOS and Android clients receive those push notifications, show them to the user, and store them for offline viewing.  Due to the design of the systems, it does not store messages on the servers once they have been reliably received by the device client.

## Configuration
### Simple
The simplest Pushover plugin configuration requires only the user key (`userkey`) and API key (`apikey`).  This will broadcast the notification to all registered devices.

#### Example
```
pushover:
  userkey: USERKEY
  apikey: APIKEY
```

### Advanced
More advanced configuration provides the ability to:

* Target a specific device (`device`)
* Set the notification message title (`title`)
* Set the notification message body (`message`)
* Set the notification priority (`priority`)
* Set the URL sent in the notification (`url`)
* Set the title of the URL (`url_title`)
* Set the default sound (`sound`)
* Set number of times to retry notifications. Relevant only from Emergency priority notification. (`retry`)
* Set time until notification expires if not acknowledged. Relevant only from Emergency priority notification.  (`expire`)
* Set a callback URL to receive acknowledgements. Relevant only from Emergency priority notification. (`callback`)
* Use multiple userkeys (`userkey`)
* Style the notification using HTML tags. (`html`)

 `device`: (string) device name as specified in the Pushover configuration  
 `title`: (string) Notification title   
 `message`: (string) Messages text  
 `priority`: (int) -1 = low, 0 = default, 1 = high, 2=Emergency  
 `url`: (string) URL Represenation text   
 `url_title`: (string) Text to be displayed as URL title
 `sound`:  (string) Should be one of [pushover's options](https://pushover.net/api#sounds).  
 `retry`: (int) Number of seconds between notifications retries. Relevant only if priority is set to 2.   
 `expire`: (int) Number of seconds to keep notification alive. Relevant only if priority is set to 2. Minimum value is 30. Maximum value is 86400.  
 `callback`: (url) A callback URL to receive acknowledgement from notifications. Relevant only if priority is set to 2.  
 `html`: (boolean) Formats the messages with HTML tags. Requires Pushover device version to be 2.3 or higher.

#### Example
```yaml
pushover:
  userkey: 
    - o23ywmAaaxTYxn00jY2JAwQ2EeYXGt    
    - 0ydnaF3023jKadfkja9fjdkjaXfdfsaySGa
  apikey: nqC2fSOLCEyHHJcnusQtw4wqG2WbWf
  device: mobile
  title: Downloading {{series_name}}
  message: Episode {{series_id}}
  priority: 2
  url: http://server.example.com/path/to/downloader/ui
  sound: incoming
  retry: 60
  expire: 1000
```

#### Example with Jinja2 tags
```yaml
pushover:
  userkey: '{{secrets.credentials.pushover.userkey}}'
  apikey: '{{secrets.credentials.pushover.apikey}}'
  sound: bike
  title: >
    {%if task in ["task_a","task_b"](/"task_a","task_b")%} New movie added to queue
    {%else%}Download Started from task {{task}}
    {%endif%}
  message: >
    {% if series_name is defined %}{{series_name}} - {{series_id}} - {{trakt_ep_name}} - {{quality|d('')}}
    {% elif imdb_name is defined%}{{movie_name}} - {{quality}}
    {% else %}{{title}}
    {% endif %}
  url: '{{trakt_series_trakt_url|d(imdb_url)}}'
  url_title: Link
  priority: >
    {% if task == "retreive_from_couchpotato" %}-1
    {% else %}0
    {% endif %}
```
#### Example with HTML tags
```yaml
pushover:
  userkey: '{{secrets.credentials.pushover.userkey}}'
  apikey: '{{secrets.credentials.pushover.apikey}}'
  html: yes
  message: |+
    <b>word</b> - display word in bold
    <i>word</i> - display word in italics
    <u>word</u> - display word underlined
    <font color="blue">word</font> - display word in blue text (most colors and   hex codes permitted)
    <a href="http://example.com/">word</a> - display word as a tappable link to http://example.com/
```
### Attachments
* [72x72px png FlexGet logo for pushover](/attachments/Plugins/pushover/flexget_logo.png)