# HorribleSubs

<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon glyphicon-download-alt"></span>
  &nbsp;
This plugin requires the cfscrape Python library. To install it, run the following command:
<br/><br/>

```cmd
pip install cfscrape
```

  <span class="glyphicon glyphicon glyphicon glyphicon-exclamation-sign"></span>
  &nbsp;
The author of Cloudflare-Scrape does not guarantee 100% safety against malicious attacks targetting any vulnerability in Cloudflare-Scrape. Precautions have been taken, but nothing is ever really safe when executing arbitrary code.

  <span class="glyphicon glyphicon glyphicon glyphicon glyphicon-info-sign"></span>
  &nbsp;
When Cloudflare updates its anti-bot measures, this plugin may cease to function. Upgraded version (if available) can be installed with:
<br/><br/>

```cmd
pip install --upgrade cfscrape
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