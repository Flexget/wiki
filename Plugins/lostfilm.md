# Lostfilm plugin
This plugin get torrents from new rss feed. Make sure you have  _lf_session_ in cookie.

Usage

```
lostfilm: yes
```
or advanced
```
lostfilm:
  url: rss_url_here
```

Example config
```
tasks:
  lostfilm:
    headers:
      cookie: lf_session=532656b1724450ccdfc62e4316b862cf;
    lostfilm: yes
    series:
      '1080p':
        - 'Stranger Things':
            alternate_name: 'Загадочные события'
```