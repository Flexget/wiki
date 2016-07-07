# Download From The Pirate Bay
The default handling of magnet links with the html plugin tries to generate a title from
the url, but sometimes results in duplicates. The following extracts the title from the dn=
field, which is more readable and reliable.

```
tasks:
  thepiratebay:
    html:
      url: http://pirateproxy.net/search/SEARCH_TERMS/0/99/0
      title_from: url
      links_re: [ magnet ]
    manipulate:
      - title:
          from: url
          extract: '&dn=([^&](/^&)+)'
    accept_all: yes
    transmission: yes
    archive: yes
```

Uses [Plugins/manipulate](/Plugins/manipulate), [Plugins/html](/Plugins/html)

[Back to The Cookbook](/Cookbook)