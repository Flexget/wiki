# Lostfilm plugin
This plugin get torrents from new rss feed. Make sure you have _uid, pass, usess, lf_session_ in cookie.

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
      cookie: uid=XXXXXX; pass=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX; usess=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX; lf_session=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX;
    lostfilm: yes
    series:
      '1080p':
        - 'Game of Thrones':
            alternate_name: 'Игра престолов'
```