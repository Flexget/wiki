= Pushover =
Available since [http://flexget.com/changeset/3203 r3203].

== Overview ==
This plugin provides the ability to send flexget notifications via the cross-platform notification system called [http://pushover.net/ Pushover].

> Pushover is a platform for sending and receiving push notifications.  On the server end, it provides an HTTP API for queueing messages to deliver to clients. On the client end, the iOS and Android clients receive those push notifications, show them to the user, and store them for offline viewing.  Due to the design of the systems, it does not store messages on the servers once they have been reliably received by the device client.

== Configuration ==
=== Simple ===
The simplest Pushover plugin configuration requires only the user key (`userkey`) and API key (`apikey`).  This will broadcast the notification to all registered devices.
==== Example ====
{{{
pushover:
  userkey: o23ywmAaaxTYxn00jY2JAwQ2EeYXGt
  apikey: nqC2fSOLCEyHHJcnusQtw4wqG2WbWf
}}}

=== Advanced ===
More advanced configuration provides the ability to:
* target a specific device (`device`)
* override the notification message title (`title`)
* override the notification message body (`message`)
* override the notification priority (`priority`)
* override the URL sent in the notification (`url`)
* override the default sound (`sound`)
* set number of times to retry notifications. Relevant only from Emergency priority notification. (`retry`)
* set time until notification expires if not acknowledged. Relevant only if priority is set to 2.  (`expire`)
* set a callback URL to receive acknowledgements. Relevant only if priority is set to 2. (`callback`)
* use multiple userkeys with a list for (`userkey`)

 device::
  (string) device name as specified in the Pushover configuration
 title::
  (string) accepts Jinja2 tags
 message::
  (string) accepts Jinja2 tags
 priority::
  (int) -1 = low, 0 = default, 1 = high, 2=Emergency - accepts Jinja2 tags
 url::
  (string) accepts Jinja2 tags
 sound::
   (string) Should be one of [https://pushover.net/api#sounds pushover's options]. Accepts Jinja2 tags 
 retry::
   (int) Number of seconds between notifications retries. Relevant only if priority is set to 2. 
 expire::
   (int) Number of seconds to keep notification alive. Relevant only if priority is set to 2. Minimum value is 30.  
 callback::
   (url) A callback URL to receive acknowledgement from notifications. Relevant only if priority is set to 2. Maximum value is 86400

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
  priority: 2
  url: http://server.example.com/path/to/downloader/ui
  sound: incoming
  retry: 60
  expire: 1000
}}}

==== Example with Jinja2 tags ====
{{{
pushover:
  userkey: '{{secrets.credentials.pushover.userkey}}'
  apikey: '{{secrets.credentials.pushover.apikey}}'
  sound: bike
  title: >
    {%if task in ["task_a","task_b"]%} New movie added to queue
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
}}}