# HorribleSubs

<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon glyphicon-download-alt"></span>
  &nbsp;
This plugin requires the cfscrape Python library. To install it, run the following command:
<br/><br/>

```cmd
pip install cfscrape
```
</div>

This plugin works as an input and as a search backend.

## Examples

### As plain input

```yaml
horriblesubs: yes
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