# Search_rss
Many website allow the generation of rss feeds based on a query. This plugin takes advantage of this can generate rss feeds that contain the result of a query.

**NOTE:** This plugin can not be used on the feed level and that it can only be used within [discover](/Plugins/discover) & [urlrewrite_search](/Plugins/urlrewrite_search) plugin.


## Config Format
All valid [rss](/Plugins/rss) plugin config options are valid here, just place `{{search_term}}` into the url where the search term should go. Jinja is used with this replacement, so you can also use [jinja](/Jinja) filters to manipulate the term.

### Simple configuration

```yaml
search_rss: http://url/q={{search_term}}
```

### Complex configuration
Search_rss supports all the advanced options from [rss](/Plugins/rss)

#### Example
```yaml
search_rss:
  url: http://url/q={{search_term}}
  link:
    - link
    - magneturi
```

## Usage example
This example shows search_rss used within the [discover](/Plugins/discover) plugin. This particular example makes use of isohunt.com and generates an rss feed with the content of a search for each movie in the queue and generates entries from that rss feed. 

```yaml
discover:
  what:
    - emit_movie_queue: yes
  from:
    - search_rss: http://isohunt.com/js/rss/{{search_term}}?iht=
```

For more information about the usage see this [recipe](/Cookbook/Movies/discoverfeed).
