# Common pitfalls and answers
## `mapping values are not allowed here, line x column y`
**Solution A: You have `:` somewhere where it's not allowed.**  
If you have `:` in example series name, you must put name in quotes.

```yaml
series:
  - name
      path: ~/name/
```

**Reason:** Name is missing `:` at the end.


**Solution B: Indentation error.**  
Thumb rule is that every time line ends with `:`next line must be indented either 2 spaces more or less.

This is ****invalid****

```yaml
series:
  - name:
    watched:
      season: 1
```

It should be:

```yaml
series:
  - name:
      watched:
        season: 1
```

Note that you need to use an extra indentation (kind of) after a line that starts with a dash (-) and ends with a colon (:).

## `ValueError: unsupported format character '"' (0x22) at ....`
In case you are using RSS input, try forcing it into ASCII.

```yaml
rss:
  url: http://example.com
  ascii: yes
```

## `RSS Feed ... is not valid XML`
Two possibilities, you're not receiving RSS feed for some reason (ie. must be logged in, cookies). Or the feed server sends is made by monkeys and isn't well formed XML. You can use [this service](http://validator.w3.org/feed/) to check if the feed is broken.

## `cron job did not run` 
* Check that you have working mail system so you receive errors occur during crontab execution.
* Add the following to the top of the crontab (crontab -e) that runs flexget so you receive cron errors to the right email address.
  * ` MAILTO="youremail@address.com" `
* Ensure the configuration file is within ~/.flexget/ and that the directory and config.yml files are owned by or at least readable by the user for which the cron is for.

## `Error in the cookie files`
If you get an error like: 

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

## `Distribution Not Found`
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

This may happen when you upgrade your linux distribution and python version gets replaced with newer one, for example 2.6 with 2.7. Now when you try to run `flexget` command it will use newer version of python and FlexGet is not installed on that. To fix the problem just reinstall FlexGet.