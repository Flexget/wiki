= !MyEpisodes =

Marks a series episode as acquired in your myepisodes.com account.

'''Simple Example'''

Most shows are recognized automatically from their TVDBname. And of course the plugin needs to know your !MyEpisodes account details.

{{{
myepisodes:
  username: <username>
  password: <password>
series:
  - human target
  - chuck
}}}

'''Advanced Example'''

In some cases, the TVDB name is either not unique or won't even be discovered. In that case you need to specify the !MyEpisodes id manually using the set plugin.

{{{
myepisodes:
  username: <username>
  password: <password>
series:
  - human target:
      set:
        myepisodes_id: 5111 
  - chuck
}}}
 
Have a look at the attached image for how to find the correct series ID on the !MyEpisodes homepage. 

== Usage without series related plugins ==

Myepisodes plugin needs certain entry fields in order to work properly, namely series_name, series_season and series_episode. When you use [wiki:Plugins/series series] plugin or related they are available automatically. If you want to use myepisode plugin with pure regexp or accept_all you must enable [wiki:Plugins/metainfo_series metainfo_series] which will try to guess those fields.

'''Example'''

{{{
rss: <url>
accept_all: yes
metainfo_series: yes
myepisodes:
  username: <username>
  password: <password>
}}}