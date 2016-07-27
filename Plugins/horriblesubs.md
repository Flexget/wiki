# HorribleSubs

This plugin works as an input and as a search backend.

Input latest releases:

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
         - next_series_episodes: anime
       from:
         - horriblesubs: yes
```

See [discover](Plugins/discover) for more information.