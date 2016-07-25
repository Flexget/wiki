# Newnzab plugin
The newznab plugins is used in conjunction with the [discover](/Plugins/discover) plugins.

With the [next_series_episodes](/Plugins/next_series_episodes)
```
discover:
  what:
    - next_series_episodes: yes
  from: 
    - newnab:
```

or the [movie_list](/Plugins/List/movie_list)

```
discover:
  what:
    - movie_list: movies
  from: 
    - newnab:
```


You need then to configure the newznab plugins, which take 4 parameters :
- website: website of the newznab server
- apikey:  mosst newznab requires this key in order to make search on their website
- category: type of search to do on newznab tv or movie
- wait  interval between two newznab call : (default  30 seconds)