## Search Plugin: sceneaccess
All the information of how sceneaccess works can be found in the plugin doc inside Flexget.

**Plugin Documentation (as of 2015-07-29)**
```
flexget doc scenaccess
```
```
Scene Access Search plugin

== Basic usage:

sceneaccess:
    username: XXXX              (required)
    password: XXXX              (required)
    category: Movies/x264       (optional)
    gravity_multiplier: 200     (optional)

== Categories:
+---------------+----------------+-----------+--------------+--------------+----------+
|    browse     |    nonscene    | mp3/0day  |   archive    |   foreign    |   xxx    |
+---------------+----------------+-----------+--------------+--------------+----------+
| APPS/ISO      | Movies/HD-x264 | 0DAY/APPS | Games/Packs  | Movies/DVD-R | XXX/0DAY |
| DOX           | Movies/SD-x264 | FLAC      | Movies/Packs | Movies/x264  | XXX/x264 |
| Games/PC      | Movies/XviD    | MP3       | Music/Packs  | Movies/XviD  | XXX/XviD |
| Games/PS3     | TV/HD          | MVID      | TV/Packs     | TV/x264      |          |
| Games/PSP     | TV/SD          |           | XXX/Packs    | TV/XviD      |          |
| Games/WII     |                |           |              |              |          |
| Games/XBOX360 |                |           |              |              |          |
| MISC          |                |           |              |              |          |
| Movies/DVD-R  |                |           |              |              |          |
| Movies/x264   |                |           |              |              |          |
| Movies/XviD   |                |           |              |              |          |
| TV/HD-x264    |                |           |              |              |          |
| TV/SD-x264    |                |           |              |              |          |
| TV/XviD       |                |           |              |              |          |
+---------------+----------------+-----------+--------------+--------------+----------+

You can combine the categories almost any way you want, here are some examples:

category:
  archive: yes          => Will search all categories within archive section

category: Movies/x264   => Search Movies/x264 within 'browse' section (browse is always default if unspecified)

category:
  browse:
    - 22  => This is custom category ID
    - Movies/XviD
  foreign:
    - Movies/x264
    - Movies/XviD

Specifying specific category ID is also possible, you can extract ID from URL, for example
if you hover or click on category on the site you'll see similar address:

http://sceneaccess.URL/browse?cat=22

In this example, according to this bit ?cat=22 , category id is 22.

== Priority

gravity_multiplier is optional parameter that increases odds of downloading found matches from sceneaccess
instead of other search providers, that may have higer odds due to their higher number of peers.
Although sceneaccess does not have many peers as some public trackers, the torrents are usually faster.
By default, Flexget give higher priority to found matches according to following formula:

gravity = number of seeds * 2 + number of leechers

gravity_multiplier will multiply the above number by specified amount.
If you use public trackers for searches, you may want to use this feature.

```


**Work-arounds / Fixes**

* To access Sceneaccess successfully through CloudFlare you will need to apply the work-around in the comments of this ticket: https://flexget.com/ticket/2897

* Make sure you are running python 2.7.9, 2.7.8 (and possibly lower) will cause SSL issues.