---
title: PitFalls
description: 
published: true
date: 2022-09-18T04:51:10.738Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:08.067Z
---

# Common pitfalls and answers
### `mapping values are not allowed here, line x column y`
**Possible cause**: You have `:` somewhere where it's not allowed.

If a series has `:` in the name, you must put the name in quotes.

**Possible cause**: `name` is missing `:` after it in the below example.

```yaml
series:
  - name
      path: ~/name/
```


**Possible cause**: Indentation error.

The rule of thumb is that every time a line ends with `:`, the next line must be indented two spaces more _from the start of the word on the previous line_. This means that for keys in lists, you don't indent two spaces from the start of the `-` (dash) on the previous line.

This is **invalid**:

```yaml
series:
  - name:
    watched:
      season: 1
```

This is **fixed**:

```yaml
series:
  - name:
      watched:
        season: 1
```
<br >

### `ValueError: unsupported format character '"' (0x22) at ....`
In case you are using an RSS input, try forcing it into ASCII.

```yaml
rss:
  url: http://example.com
  ascii: yes
```

<br>

### `RSS Feed ... is not valid XML`
**Possible cause**: You're not receiving an RSS feed for some reason (i.e. you must be logged in, missing cookies, etc.).

**Possible cause**: The feed server sends is made by monkeys and isn't outputting well-formed XML. You can use [this service](http://validator.w3.org/feed/) to check if the feed is broken.

<br>

### `cron job did not run` 
**Possible cause**: Check that you have a working mail system so you receive errors occur during crontab execution.
* Add the following to the top of the crontab (crontab -e) that runs flexget so you receive cron errors to the right email address.
  * ` MAILTO="youremail@address.com" `

**Possible cause**: Ensure the configuration file is within `~/.flexget/` and that the directory and `config.yml` is owned by, or at least readable by, the user under which cron is operating.

<br>

### `cookielib bug`
If you get an error like this: 

```
/usr/lib/python2.6/_MozillaCookieJar.py:109: UserWarning: cookielib bug!
Traceback (most recent call last):
  File "/usr/lib/python2.6/_MozillaCookieJar.py", line 82, in _really_load
    assert domain_specified == initial_dot
AssertionError

  _warn_unhandled_exception()
```

And you know your Netscape cookie file is properly formatted, but you just can't get it to work, try rewriting the cookie file with curl:

```bash
curl -b oldcookiefile.txt --cookie-jar newcookiefile.txt http://url
```

<br>

### `Distribution Not Found`
```
Traceback (most recent call last):
  File "/usr/local/bin/flexget", line 5, in <module>
    from pkg_resources import load_entry_point
  File "/usr/lib/python2.7/dist-packages/pkg_resources.py", line 2707, in <module>
    working_set.require(__requires__)
  File "/usr/lib/python2.7/dist-packages/pkg_resources.py", line 686, in require
    needed = self.resolve(parse_requirements(requirements))
  File "/usr/lib/python2.7/dist-packages/pkg_resources.py", line 584, in resolve
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: FlexGet==1.0r2175
```

This may happen when you upgrade your Linux distribution and the Python installation gets replaced with a newer one - for example 2.6 is replaced by 2.7. When you then try to run `flexget` it will use the newer version of Python, and FlexGet is not installed on that. To fix the problem, just reinstall FlexGet.