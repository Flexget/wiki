---
title: urlrewrite
description: 
published: true
date: 2022-09-18T05:16:22.353Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:19.768Z
---

# URL Rewrite
Read [how URL rewriting works](/URLRewriters).

Allows manipulating download pages into proper download URLs. If information required to generate the URL is not present, the site needs urlrewriting plugin.

**Example**

```yaml
urlrewrite:
  sitename:
    regexp: 'http://imaginary.org/tor/(?P<id>\d+)/(?P<name>.*)'
    format: 'http://imaginary.org/download/\g<id>/\g<name>'
```

This would rewrite URL

```txt
http://imaginary.org/tor/1234/test.torrent
```

to:

```txt
http://imaginary.org/download/1234/test.torrent
```

## Escaping
Few regexp characters absolutely need to be escaped with `\` (in context of urls). At least + and ? metacharacters.

**Example**

```txt
http://example.com/?id=1234
```

should be

```txt
http://example.com/\?id=(?P<id>\d+)
```