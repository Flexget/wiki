# Lostfilm plugin
This plugin gets torrents from lostfilm RSS feed. You need to get your personal value of *lf_session* cookie for lostfilm site.

### Usage

``` yaml
lostfilm: <lf_session_cookie_value>
```
Alternatively, if you already have *lf_session* set in flexget cookies, you can simply use
``` yaml
lostfilm: yes
```
Lostfilm plugin extracts original series names, therefore you need to specify original series names for [**series**](https://flexget.com/Plugins/series) plugin.
### Advanced usage
``` yaml
lostfilm:
  lf_session: "<lf_session_cookie_value>"
  prefilter: no
  site_urls:
    - "http://example.com/"
    - "https://example.org/"
```
#### Parameter *lf_session*
The *lf_session* parameter must be set to the value of the *lf_session* cookie for lostfilm site. It works as authorisation.
#### Parameter *prefilter*
This plugin reads all series names configured for the current task and extracts torrents from lostfilm's RSS feed only for configured series (as every torrent URL extraction requires two additional HTTP requests). If you want to get full list of torrents from RSS feed (and filter it later by series plugin) you can disable _prefilter_ feature (plugin will work slower and generate more network traffic).
#### Parameter *site_urls*
Lostfilm site has several mirrors and some of them may have access problems from time to time. The lostfilm plugin has built-in list of mirrors and they are tried one-by-one to find the accessible mirror. The list of URLs can be overridden by *site_urls* parameter. URLs should be specified in order of preference. Note: unlike with removed *url* parameter, do not use `/rss.xml` in URLs , it will be added automatically by plugin.

Alternatively, the multi-URL feature can be disabled by specifying the single site address:
``` yaml
lostfilm:
  lf_session: "<lf_session_cookie_value>"
  site_urls: "https://someurl.example/"
```
#### Removed parameters
Parameter *url* was removed as more advanced functionality is provided by *site_urls* parameter.
#### Additional fields
The lostfilm plugin sets additional fields for each produced entry: *series_name_org*, *series_name_rus*, *episode_name_rus*, *episode_name_org*. They can be used for notifications or for other purposes.

### Example config
``` yaml
tasks:
  download-task:
    lostfilm: "532656b1724450ccdfc62e4316b862cf"
    series:
      '1080p':
        - 'Stranger Things'
```
### [Proxy](https://flexget.com/Plugins/proxy) support
If access to lostfilm site is blocked by your ISP, you can use [**Proxy Plugin**](https://flexget.com/Plugins/proxy).