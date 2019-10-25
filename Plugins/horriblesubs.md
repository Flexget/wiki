# HorribleSubs

<div class="alert alert-warning" role=alert>

HorribleSubs no longer use cloudflare protection, **you don't** need **cfsraper** plugin to get this work correctly 
</div>
<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon glyphicon-download-alt"></span>
  &nbsp;
HorribleSubs use cloudflare protection.

This plugin requires the [cfscraper](/Plugins/cfscraper) plugin.
</div>

This plugin works as an input and as a search backend.

## Examples

### As plain input

```yaml
tasks:
  watchlist-anime:
    inputs: 
      - horriblesubs: yes
    accept_all: yes
    seen: local
```

### Discover next episodes of series

```yaml
tasks:
  search-anime:
     discover:
       what:
         - next_series_episodes: yes
       from:
         - horriblesubs: yes
```

See [discover](/Plugins/discover) and [next_series_episodes](/Plugins/next_series_episodes) for more information.