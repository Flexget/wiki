**Adrellias flexget config**

My config file is mostly based off the below users configuration.   

[atlanta800](https://github.com/atlanta800/dotfiles/tree/master/flexget) (now on github, old page [here](/Cookbook/UserAtlanta800))::

He has a lot of just sane settings! I wanted a automated setup that someone that does not know how to, add things to a config file could use. 
A spouse for instance. So my config uses [http://trakt.tv/](/http://trakt.tv/) to generate rss based searches without having to add the new series to a config file every time. 

So i use the discover plugin with trakt_list to generate input feeds rss searches dynamically.

This is just a extract of what i have changed in atlanta800's config file

```
# This template is a "global" template for all TV-related feeds.
  # We keep all of the RSS feeds that list tv-related torrents here
  # as well as where to check existing shows.
  tv-global:
    # This will search my trakt.tv custom list called tvshows and then use search_rss to search for those shows 
    discover:
      what:
        - trakt_list:
        # Use trakt.tv watchlist to get series names 
            username: trakusername
            password: trakpassword
            api_key: trakapikey
            custom: tvshows
            strip_dates: yes
      from:
        # Then search ezrss for the shows found in the watchlist - This could do away with series.yml
        - search_rss: https://www.ezrss.it/search/index.php?show_name=\{{search_term}}&mode=rss
        - search_rss: http://torrentz.eu/feed?q=\{{search_term}}
        #- search_rss: http://kat.ph/search/\{{search_term}}/?rss=1 # This feed seems to have alot of mixed languages
      type: any
```

This is the only thing i have in my tasks for series.


```
# This is where we pull everything together
tasks:

  # All of the TV-related feeds pull in the tv-global template, this gives
  # all of the necessary rss sources and a few extra configs

  Auto_TV_Shows:
    priority: 1
    template:
      - tv-global
      - tv-my_shows
    import_series:
      # Import the series showed in the watch list so their seen as valid series
      from:
        trakt_list:
          username: trakusername
          password: trakpassword
          api_key: trakapi
          custom: tvshows
          strip_dates: yes
      settings:
        quality: hdtv <=720p
        propers: no
```
