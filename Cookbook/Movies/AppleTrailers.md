# Downloading Apple Trailers
### Quick Start
 [Apple Trailers Plugin](/Plugins/apple_trailers)::

### Downloading Trailers By Genre
This method involves looking up movie titles through the [imdb](/Plugins/imdb) plugin. It then filters out the genres you don't want included. In the example below, the genres of Documentary, Foreign, Comedy, Fantasy, or Musical were rejected.

```
AppleTrailers:
  apple_trailers: 720p
  imdb:
    reject_genres:
      - documentary
      - foreign
      - comedy
      - fantasy
      - musical
  download: J:\FTP\Trailers
  set:
    filename: '{{title}} - Trailer - 720p.mov'
  seen: local  # We don't want accepted entries from this feed to affect actual movie download feeds.
```


[Back to The Cookbook](/Cookbook)