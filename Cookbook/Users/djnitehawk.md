this is my personal config.yml which does the following:

* download tv shows that's in a custom trakt.tv list.
* uses utorrent as the client to download torrents.
* uses multiple rss feeds per template.
* tv shows are downloaded in 720p resolution.

replace everything in ALL_CAPS with your relevant information and you should be good to go.

{{{
templates:
  tv:
    utorrent:
      url: http://localhost:8080/gui/
      username: rachaelellen7
      password: cristal7
      path: C:\Users\Alex\Downloads\TV Shows
    configure_series:
      settings:
        quality: 720p
        propers: no
      from:
        trakt_list:
          username: rachaelellen7
          api_key: 58582179fbfd2014508327bc37170e01
          custom: showsiwatch
          strip_dates: yes
    content_size:
      min: 400
      max: 2000
      strict: no
    inputs:
      - rss: http://rss.thepiratebay.se/208
      - rss: https://kickass.to/tv/?rss=1
      - rss: http://torrentz.eu/feed?verified&q=tv%20shows

tasks:
  TV-SHOWS:
    template: tv
    priority: 1
}}}