= pyLoad =

Output plugin for [http://pyload.org pyLoad] download manager.


----
== Features ==
  * Scan the accepted feeds for urls
  * Scan the feed's html page for additional urls
  * Check for prefered hoster
  * Add found links as package to pyLoad



----
== Prerequisites ==
Make sure [http://pyload.org pyLoad] is running and you have at least version '''0.4.9'''. The webinterface needs to be activated and accessible, so FlexGet can use the API.



----
== Configuration ==

'''Example:'''

{{{
pyload:
  api: http://localhost:8000/api
  username: <user>
  password: <pwd>
  package: <package>
  folder: <folder>
  queue: [yes|no]
  parse_url: [yes|no]
  hoster:
    - List of prefered Hoster
  multiple_hoster: [yes|no]
  enabled: [yes|no]
}}}

Default values for the config elements:
{{{
pyload:
  api: http://localhost:8000/api
  queue: yes
  parse_url: no
  hoster: ALL
  multiple_hoster: yes
  enabled: yes
}}}

[[br]]
=== API Access ===

The '''api''' parameter should be the address of the webinterface followed by "/api", in case the webinterface runs locally on port 8000 the default value will suffice.
Don't forget to set the correct '''username''' and '''password'''.

[[br]]
=== How to Add Downloads ===

You can define the naming format for the packages to be added with every entry by specifying the '''package''' parameter accordingly. It is [http://flexget.com/wiki/Jinja Jinja] enabled and, therefore, allows for a dynamic formatting by applying the [http://flexget.com/wiki/Entry entry]'s field values.
For example, the following will result in packages like "The Walking Dead - S01E05":
{{{
pyload:
  ...
  package: '{{series_name}} - {{series_id}}'
  ...
}}}

If no package formatting is defined, Flexget uses the name of the entry.

[[br]]
This is not yet possible for the definition of the '''folder''' parameter, which can be used to define a certain download folder. When no folder is supplied pyload will choose the folder name (Usually the package name).

The '''queue''' parameter specifies whether new packages should be queued immediately or added to the collection instead.

[[br]]
=== Hosters and URL Parsing  ===

By default this plugin will accept all hoster, if you want to filter prefered ones lookup the names at pyloads [http://pyload.org/hoster plugin overview] first.
Then simply create a list like this:
{{{
hoster:
  - YoutubeCom
  - MyvideoDe
}}}

When a prefered hoster is found only these links will be added, if not remaining hosters gets added.
To only add the first found prefered hoster set '''multiple_hoster''' to off.

If '''queue''' is activated downloads will start immediately, otherwise go to collector and wait for user interaction.

When '''parse_url''' is activated pyload will load the html page at the feed url and check it for additional links. This is useful for hoster who don't include any links in the feed content. This requires that the feed url to link at an article or page related to the entry and '''not''' on a general page or front page. You should first make sure that this is the case so no wrong links gets added.