= pyLoad =

Output plugin for [http://pyload.org pyLoad] download manager.

== Features ==
  * Scan the accepted feeds for urls
  * Check for prefered hoster
  * Add found links as package to pyLoad


'''Example:'''

{{{
pyload:
  api: http://localhost:8000/api
  queue: [yes|no]
  username: <user>
  password: <pwd>
  hoster:
    - List of prefered Hoster
  multihoster: [yes|no]
  enabled: [yes|no]
}}}

Default values for the config elements:

{{{
pyload:
  api: http://localhost:8000/api
  queue: yes
  hoster: ALL
  multihoster: yes
  enabled: yes
}}}

== Prerequisites ==
Make sure [http://pyload.org pyLoad] is running and you have at least version '''0.4.8'''. The webinterface needs to be activated and accessible, so FlexGet can use the API.

The '''api''' parameter should be the address of the webinterface followed by "/api", in case the webinterface runs locally on port 8000 the default value will be ok.
Don't forget to set correct '''username''' and '''password'''.

== Configuration == 

By default this plugin will accept all hoster, if you want to filter prefered ones lookup the names at pyloads [http://pyload.org/hoster plugin overview] first.
Then simply create a list like this:
{{{
hoster:
  - YoutubeCom
  - MyvideoDe
}}}

When a prefered hoster is found only these links will be added, if not remaining hosters gets added.
To only add the first found prefered hoster set '''multihoster''' to off.

If '''queue''' is activated downloads will start immediately, otherwise go to collector and wait for user interaction.