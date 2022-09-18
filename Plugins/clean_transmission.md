---
title: clean_transmission
description: 
published: true
date: 2022-09-18T05:02:51.469Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:02:48.807Z
---

# Clean Transmission

<div class="alert alert-warning" role="alert">
<span class="glyphicon glyphicon-exclamation-sign"></span>
  &nbsp;
This plugin has been deprecated as of FlexGet 2.20 See <a href="/Cookbook/TorrentCleanup">this</a> cookbook entry for a replacement.
</div>

This plugin cleans the Transmission's queue of finished torrents (=the torrents that have completed the download process and are in **stopped, finished or seeding** state).

This plugin requires the transmission-rpc library. To install it, run:

```
pip install transmission-rpc
```

You may be required to upgrade transmission-rpc after upgrading transmission, for that just add `--upgrade` to the previous command.

## Config settings

| **Name** | **Info** | **Description** |
| --- | --- | --- |
| host | Text | Where transmission is listening (default: localhost) |
| port | Number | Connected port (default: 9091) |
| netrc | File |  |
| username | Text |  |
| password | Text |  |
| finished_for | Interval | (optional) remove only torrents finished for at least the specified time (1 hours, 2 days, etc). |
| min_ratio | Number | (optional) remove only torrents uploaded at least this ratio (0=0%, 0.5=50%, 1=100% etc) |
| tracker | RegExp | (optional) remove only torrents that contain a tracker hostname matching this [regular expression](https://docs.python.org/2/library/re.html#regular-expression-syntax) |
| preserve_tracker | RegExp | (optional) remove only torrents that do not contain a tracker hostname matching this [regular expression](https://docs.python.org/2/library/re.html#regular-expression-syntax) |
| directories | RegExp List | (optional) remove only torrents with a download directory that matches one of the regular expressions in the list |
| delete_files | [Yes\|No] | (optional) also delete local files (default: no) |
| transmission_seed_limits | [Yes\|No] | (optional) uses transmission's internal limits for idle time and seed ratio (default: no) |
| enabled | [Yes\|No] | Plugin enabled (default: yes) |

**Note:**

- If `finished_for` and/or `min_ratio` parameters are defined, all the finished torrents meeting one or both the conditions will be removed.
- The `tracker` regular expression will match any part of a tracker's hostname. Use `^` or `$` to restrict matching to the beginning or end of hostnames (e.g. `\.se$` to match only trackers under the Swedish top-level domain).
- The `preserve_tracker` regular expression works in the same manner as the `tracker` setting. Both settings can be used in conjunction to provide a high degree of filtering. 
- From flexget 1.2.190 and up you need to set `transmission_seed_limits: yes` to get the same behaviour as previous version of this plugin or torrents may not be removed when completed.


## Examples
`clean_transmission` triggers default warnings that will be shown in flexget.log. `disable: details` disables those warnings, but it's better to leave it in if you don't care about the extra clutter (it may hide actual problems). 

```
clean_transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
  finished_for: 2 hours
  tracker: nyaa|animebytes
  preserve_tracker: alpharatio|32pag
disable: details
```

In the example below we illustrate how we can remove torrents based on their download directory. It will remove all torrents under `/media/beta/Downloads/Shows/Auto` and its sub-directories that have finished for at least 2 hours.

```
clean_transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
  finished_for: 2 hours
  directories:
    - \A/+media/+beta/+Downloads/+Shows/+Auto(\Z|/+.*)
disable: details
```

Note that you can combine both `directories` and `tracker` in the previous examples

```
clean_transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
  finished_for: 2 hours
  tracker: nyaa|animebytes
  directories:
    - \A/+media/+beta/+Downloads/+Shows/+Auto(\Z|/+.*)
disable: details
```

This would remove all torrents under `/media/beta/Downloads/Shows/Auto` and its sub-directories that have finished for at least 2 hours that were downloaded from `nyaa` or `animebytes`.
