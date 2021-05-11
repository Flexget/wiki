# Lostfilm plugin
This plugin gets torrents from lostfilm RSS feed. You need to get your personal value of _lf_session_ cookie for lostfilm site.

### Usage

```
lostfilm: <lf_session_cookie_value>
```
If you already have _lf_session_ set in flexget cookies, you can simply use
```
lostfilm: yes
```
### Advanced usage
```
lostfilm:
  url: <rss_feed_url>
  lf_session: <lf_session_cookie_value>
  prefilter: no
```
Custom URL for RSS feed can be configured.

This plugin reads all series names configured for current task and extracts torrents only for configured series (as every torrent URL requires two additional HTTP requests). If you want to get full list of torrents from RSS feed (and filter it later by series plugin) you can disable _prefilter_ feature (plugin will work slower and generate more network traffic).

### Example config
```
tasks:
  lostfilm:
    lostfilm: 532656b1724450ccdfc62e4316b862cf
    series:
      '1080p':
        - 'Stranger Things'
```
### Proxy support
If access to lostfilm site is blocked by your ISP, you can use [Proxy Plugin](https://flexget.com/Plugins/proxy).