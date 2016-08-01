# HorribleSubs

This plugin works as an input and as a search backend.

#### Example as input:

```yaml
horriblesubs: yes
```

#### Example with discover:

```yaml
tasks:
  search-anime:
     discover:
       what:
         - next_series_episodes: yes
       from:
         - horriblesubs: yes
```

See [discover](Plugins/discover) and [next_series_episodes](Plugins/next_series_episodes) for more information.