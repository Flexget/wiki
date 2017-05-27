# Movie Queue Input
_**IMPORTANT**_: `movie_queue` was removed and replaced with the [movie_list](/Plugins/List/movie_list) plugin in v2.3.0. This information is no longer maintained and is only kept for historical purposes.

Creates an [Entry](/Entry) for each movie in your [movie queue](/Plugins/movie_queue) (intended to be used with the [discover](/Plugins/discover) plugin).

### Example
```
discover:
  what:
  - emit_movie_queue: yes
  from:
  - torrentz: verified
movie_queue: accept
```

You should almost certainly use movie_queue: yes with this, like below.

```
movie_queue: yes
```

### Queue names
If movies were added to [movie queue](/Plugins/movie_queue) using a queue name, you emit from that queue by using `queue_name`:
```
discover:
  what:
  - emit_movie_queue:
      queue_name: a queue name
  from:
  - torrentz: verified
movie_queue: accept
```

### Notes
 * `queue_name` is case insensitive
 * Emits names in IMDB translated form, making this pretty useless with [search](/Plugins/search) if you live somewhere where english isn't primary language. A workaround for this problem is to make sure that you use the [imdb_list](/Plugins/imdb_list) plugin with username and password and then go to your imdb account and update your site preferences to "Title display country" as "United states" and "Title display language" as English.