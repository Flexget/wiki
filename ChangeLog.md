# Changelog
This changelog is in progress. It can be manually updated via the wiki, but is also updated automatically via select commit messages and new releases. The two comment lines with git hashes (`<!---a1234--->`) must not be changed or removed.

<!---c1b2c3ecfd7879e9b848558cb51921e037c58918--->

## 2.10.27.dev (unreleased)
### Fixed
- trakt_list - Fixed crash on missing key. Fixes [#1745](https://github.com/Flexget/Flexget/issues/1745)
- telegram - Handled edited messages in bot updates. Fixes [#1768](https://github.com/Flexget/Flexget/issues/1768)

<!---1865c4c7ae37db20195ee3e83f9d5b93d2c69ebb--->

## 2.10.26 (2017-04-04)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.25...2.10.26)
### Added
- Series [season pack](Plugins/series/season_packs) support

## 2.10.25 (2017-04-02)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.24...2.10.25)

## 2.10.24 (2017-03-29)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.23...2.10.24)
### Fixed
- email - Fix issue with persistent connection between tasks and wrong config usage. Closes [#1761](https://github.com/Flexget/Flexget/issues/1761)
- series - Fix correct comparison for special episodes. Closed [#1592](https://github.com/Flexget/Flexget/issues/1592)


## 2.10.23 (2017-03-28)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.22...2.10.23)
### Fixed
- rutracker - Made url match based on regexp
- email - Keep smtp server connection open between notifications. Fixes [#1751](https://github.com/Flexget/Flexget/issues/1751)


## 2.10.22 (2017-03-26)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.21...2.10.22)
### Fixed
- move: no longer crashes on permission errors, fixes [#1747](https://github.com/Flexget/Flexget/issues/1747)
- lostfilm - link changed on site ([#1753](https://github.com/Flexget/Flexget/issues/1753))


## 2.10.21 (2017-03-25)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.20...2.10.21)

## 2.10.20 (2017-03-24)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.19...2.10.20)
### Fixed
- join - Fixed after api change, api_key is now mandatory. Closed [#1746](https://github.com/Flexget/Flexget/issues/1746)


## 2.10.19 (2017-03-22)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.18...2.10.19)
### Changed
- Extend series list help message. ([#1720](https://github.com/Flexget/Flexget/issues/1720)) ([#1737](https://github.com/Flexget/Flexget/issues/1737))


## 2.10.18 (2017-03-19)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.17...2.10.18)

## 2.10.17 (2017-03-18)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.16...2.10.17)

## 2.10.16 (2017-03-17)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.15...2.10.16)
### Added
- *  mirrors for rutracker plugin
- mirrors for rutracker plugin ([#1736](https://github.com/Flexget/Flexget/issues/1736))


## 2.10.15 (2017-03-16)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.14...2.10.15)
### Changed
- delete - Call log.warning instead of raising PluginWarning ([#1723](https://github.com/Flexget/Flexget/issues/1723))
- use https ([#1724](https://github.com/Flexget/Flexget/issues/1724))

### Fixed
- clean_transmission: yes now does something
- strip _id suffix of query params ([#1724](https://github.com/Flexget/Flexget/issues/1724))


## 2.10.14 (2017-03-14)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.13...2.10.14)
### Fixed
- notify - Fixed an issue whe trying to notify both to `notify` and `task` scope. Fixes [#1726](https://github.com/Flexget/Flexget/issues/1726)


## 2.10.13 (2017-03-13)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.12...2.10.13)
### Fixed
- Fixed UI building process, fixes [#1731](https://github.com/Flexget/Flexget/issues/1731)


## 2.10.12 (2017-03-11)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.11...2.10.12)
### Fixed
- morethantv: site endlessly redirects when cookie is invalid, fixes [#1729](https://github.com/Flexget/Flexget/issues/1729)


## 2.10.11 (2017-03-07)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.10...2.10.11)
### Fixed
- Report a config error when 'list' option is not given to next_trakt_episodes


## 2.10.10 (2017-03-02)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.9...2.10.10)
### Fixed
- plex - Fixed schema defaults. Fixed [#1713](https://github.com/Flexget/Flexget/issues/1713)


## 2.10.9 (2017-02-28)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.8...2.10.9)
### Added
- Add Pushsafer Notification Service ([#1712](https://github.com/Flexget/Flexget/issues/1712))


## 2.10.8 (2017-02-27)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.7...2.10.8)
### Fixed
- filelist: now properly attemps to grab the full title of search results
- irc: fixed compatibility with py3 (urllib)


## 2.10.7 (2017-02-25)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.6...2.10.7)
### Fixed
- filelist: fixed cookie renewal


## 2.10.6 (2017-02-23)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.5...2.10.6)
### Fixed
- irc: optional fields now default to empty string instead of None


## 2.10.5 (2017-02-22)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.4...2.10.5)
### Fixed
- btn: updated to new domain, related [#1698](https://github.com/Flexget/Flexget/issues/1698)

### Changed
- rutracker - always use https ([#1703](https://github.com/Flexget/Flexget/issues/1703))


## 2.10.4 (2017-02-21)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.3...2.10.4)
### Added
- *  jinja2 filters CLI
- jinja2 filters CLI ([#1702](https://github.com/Flexget/Flexget/issues/1702))
- NewPCT added search feature ([#1680](https://github.com/Flexget/Flexget/issues/1680))

### Fixed
- catch db vacuum crash for now. Fixes [#1596](https://github.com/Flexget/Flexget/issues/1596)


## 2.10.3 (2017-02-20)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.2...2.10.3)
### Added
- Added Entry list search ability ([#1691](https://github.com/Flexget/Flexget/issues/1691))

### Fixed
- filelist: search_in now works
- filelist: fixed search_in config type
- fixed logic in default jinja statement. Fixes [#1701](https://github.com/Flexget/Flexget/issues/1701)

### Changed
- added ability to set a custom message for task notifications
- made jinja `re_search` filter case insensitive. Closed [#1689](https://github.com/Flexget/Flexget/issues/1689)


## 2.10.2 (2017-02-19)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.1...2.10.2)
### Fixed
- morethantv: fixed a crash when login request fails
- btn: no longer crashes if the api does not return a json object, closes [#1698](https://github.com/Flexget/Flexget/issues/1698)

### Added
- filelist: new search plugin for FileList
- unique: reject/accept duplicate entries


## 2.10.1 (2017-02-18)
[all commits](https://github.com/Flexget/Flexget/compare/2.10.0...2.10.1)

## 2.10.0 (2017-02-17)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.23...2.10.0)
### Added
- Added ability to always send task scoped notifications ([#1662](https://github.com/Flexget/Flexget/issues/1662))
- *  My Anime List input plugin
- *  My Anime List input plugin ([#1629](https://github.com/Flexget/Flexget/issues/1629))
- * [UI] Config section allows editing of variables
- quality: added support for 2160p
- *  convert_magnet: new config option to fail entries if conversion fails, closes [#1619](https://github.com/Flexget/Flexget/issues/1619)
- *  subliminal: added support for .rar files
- slack - Added ability to override icon via image url

### Changed
- series parser: added support for Exx identifier
- * [UI] Username is autofilled on login page
- npo_watchlist: updated to only grab broadcasts; previously it also grabbed trailers
- piratebay: replacing single quotes with spaces as their search engine doesn't like them

### Fixed
- *  added ability to always send task scoped notification if when there's no accepted/failed entries. Closes [#1657](https://github.com/Flexget/Flexget/issues/1657)
- * [UI] Removing a show when in search mode, keeps the UI in search page [#1559](https://github.com/Flexget/Flexget/issues/1559)
- * [UI] improves version checking, fixes [#1617](https://github.com/Flexget/Flexget/issues/1617)
- *  sickbeard: fixed a typo that caused a crash when 'include_data: yes', fixes [#1623](https://github.com/Flexget/Flexget/issues/1623)
- *  est_released_movies: Fixed crash with movie_year of None ([#1602](https://github.com/Flexget/Flexget/issues/1602))


## 2.9.23 (2017-02-16)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.22...2.9.23)
### Added
- New lostfilm plugin ([#1681](https://github.com/Flexget/Flexget/issues/1681))


## 2.9.22 (2017-02-14)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.21...2.9.22)

## 2.9.21 (2017-02-13)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.20...2.9.21)
### Added
- freshon search plugin


## 2.9.20 (2017-02-12)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.19...2.9.20)
### Changed
- Update rutracker_auth plugin ([#1684](https://github.com/Flexget/Flexget/issues/1684))


## 2.9.19 (2017-02-11)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.18...2.9.19)
### Fixed
- divxatope: changed domain to divxatope1, fixes [#1601](https://github.com/Flexget/Flexget/issues/1601)
- divxatope to use new domain divxatope1 ([#1655](https://github.com/Flexget/Flexget/issues/1655))

### Added
- from_rtorrent: added `load_date` field (torrent added date)
- aria2: added filename option (known as --out parameter in aria2)

### Changed
- jinja: changed parsedate jinja filter to support more formats


## 2.9.18 (2017-02-10)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.17...2.9.18)
### Fixed
- proxies - Fixed socks5 support


## 2.9.17 (2017-02-09)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.16...2.9.17)
### Fixed
- check_subtitles: now properly finds internal subtitles
- sickbeard - Handle corrupt data from the API. Fixes [#1672](https://github.com/Flexget/Flexget/issues/1672)

### Added
- url schema format - Added sock5 as a valid protocol. Related [#992](https://github.com/Flexget/Flexget/issues/992)


## 2.9.16 (2017-02-08)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.15...2.9.16)

## 2.9.15 (2017-02-05)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.14...2.9.15)
### Fixed
- myepisodes, myepisodes_list: login check is no longer dependent on username
- rtorrent: fixed python 3 crash (UnboundLocalError) caused by try-except scope changes, fixes [#1669](https://github.com/Flexget/Flexget/issues/1669)


## 2.9.14 (2017-02-03)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.13...2.9.14)
### Fixed
- move/copy: 'along' files are now properly renamed when 'rename' contains an extension, but 'keep_extension: yes' is set


## 2.9.13 (2017-02-02)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.12...2.9.13)
### Fixed
- serienjunkies: added 'task' interface, which allows the plugin to be used in a task config
- download: no longer crashes when cleaning temp files that don't exist


## 2.9.12 (2017-02-01)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.11...2.9.12)
### Fixed
- rapidpush - Fixed message format. Closed [#1665](https://github.com/Flexget/Flexget/issues/1665)
- Update npo_watchlist ([#1664](https://github.com/Flexget/Flexget/issues/1664))


## 2.9.11 (2017-01-28)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.10...2.9.11)
### Changed
- kodi_library: default to port 8080


## 2.9.10 (2017-01-26)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.9...2.9.10)
### Fixed
- movie_list: fixed cli commands 'add' and 'del', which crashed under certain conditions, fixes [#1606](https://github.com/Flexget/Flexget/issues/1606)
- Fix crash when kodi_library encounters a network error. fix [#1653](https://github.com/Flexget/Flexget/issues/1653)
- slack - Fix setting icon_emoji. Fixes [#1649](https://github.com/Flexget/Flexget/issues/1649)


## 2.9.9 (2017-01-24)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.8...2.9.9)
### Fixed
- Stop loading all http responses into memory. fix [#1647](https://github.com/Flexget/Flexget/issues/1647)
- plugins cli - Changed `group` to `interface`. Fixes [#1650](https://github.com/Flexget/Flexget/issues/1650)
- iptorrents - Fix both crash issues mentioned in [#1643](https://github.com/Flexget/Flexget/issues/1643) ([#1651](https://github.com/Flexget/Flexget/issues/1651))


## 2.9.8 (2017-01-22)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.6...2.9.8)
### Added
- Add url rewrite support for bt.hliang.com ([#1630](https://github.com/Flexget/Flexget/issues/1630))
- imdb_watchlist: added support for choosing types ([#1645](https://github.com/Flexget/Flexget/issues/1645))
- *  toast - Added mac support

### Fixed
- T411 url has changed (still one) ([#1641](https://github.com/Flexget/Flexget/issues/1641))
- my_anime_list: coerce default status and type to lists in Python 3
- my_anime_list: added missing anime types, fixes [#1640](https://github.com/Flexget/Flexget/issues/1640)


## 2.9.6 (2017-01-17)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.5...2.9.6)
### Fixed
- Remove strictness in API trailing slashes, fixes [#1635](https://github.com/Flexget/Flexget/issues/1635)


## 2.9.5 (2017-01-16)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.4...2.9.5)
### Changed
- series parser: added support for Exx identifier

### Added
- *  My Anime List input plugin
- My Anime List input plugin ([#1629](https://github.com/Flexget/Flexget/issues/1629))


## 2.9.4 (2017-01-14)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.3...2.9.4)
### Added
- [UI] Config section allows editing of variables


## 2.9.3 (2017-01-13)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.2...2.9.3)
### Added
- quality: added support for 2160p

### Fixed
- [UI] Removing a show when in search mode, keeps the UI in search page [#1559](https://github.com/Flexget/Flexget/issues/1559)
- [UI] improves version checking, fixes [#1617](https://github.com/Flexget/Flexget/issues/1617)

### Changed
- [UI] Username is autofilled on login page


## 2.9.2 (2017-01-12)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.1...2.9.2)
### Fixed
- sickbeard: fixed a typo that caused a crash when 'include_data: yes', fixes [#1623](https://github.com/Flexget/Flexget/issues/1623)


## 2.9.1 (2017-01-11)
[all commits](https://github.com/Flexget/Flexget/compare/2.9.0...2.9.1)
### Changed
- npo_watchlist: updated to only grab broadcasts; previously it also grabbed trailers
- piratebay: replacing single quotes with spaces as their search engine doesn't like them

### Added
- convert_magnet: new config option to fail entries if conversion fails, closes [#1619](https://github.com/Flexget/Flexget/issues/1619)
- subliminal: added support for .rar files

### Fixed
- est_released_movies: Fixed crash with movie_year of None ([#1602](https://github.com/Flexget/Flexget/issues/1602))


## 2.9.0 (2017-01-10)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.24...2.9.0)
### Changed
- The notification system has been overhauled again
- Rename 'secrets' plugin to 'variables', and change usage.
- Convert `if` plugin to use jinja2 expressions instead of raw python


## 2.8.24 (2017-01-09)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.20...2.8.24)
### Fixed
- bakabt - Update URLs ([#1614](https://github.com/Flexget/Flexget/issues/1614))
- rarbg: tokens are now fetched with the same domain delay as other requests, fixes [#1560](https://github.com/Flexget/Flexget/issues/1560)

### Added
- *  new search plugin for torrentday
- new search plugin for private tracker torrentday ([#1597](https://github.com/Flexget/Flexget/issues/1597))


## 2.8.20 (2017-01-06)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.19...2.8.20)
### Fixed
- aria2 options from config file were ignored when passing a torrent file rather than uri
- Prevent crash in aria2 plugin in certain configurations. fix [#1604](https://github.com/Flexget/Flexget/issues/1604)
- convert_magnet on python 3
- convert_magnet plugin compatibility for libtorrent version <= 0.16.13.0 fix [#1514](https://github.com/Flexget/Flexget/issues/1514)
- npo_watchlist: properly strip/convert invalid Windows characters

### Changed
- Plex improvements ([#1607](https://github.com/Flexget/Flexget/issues/1607))


## 2.8.19 (2017-01-05)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.18...2.8.19)
### Changed
- trakt_list now populates trakt series/movie name and year fields


## 2.8.18 (2017-01-04)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.17...2.8.18)
### Fixed
- torrentleech - Fix torrentleech URLs after changes on the site


## 2.8.17 (2017-01-03)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.16...2.8.17)
### Fixed
- terminal - Strip spaces before new lines in porcelain style table. Fixes [#1584](https://github.com/Flexget/Flexget/issues/1584)


## 2.8.16 (2017-01-02)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.15...2.8.16)
### Added
- input plugin for kitsu.io


## 2.8.15 (2017-01-01)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.14...2.8.15)
### Fixed
- nyaa changed TLD from .eu to .se
- bakabt changed TLDs from .com to .me
- nyaa changed TLD


## 2.8.14 (2016-12-29)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.13...2.8.14)
### Fixed
- npo_watchlist: words in dates are now properly parsed, fixes [#1588](https://github.com/Flexget/Flexget/issues/1588)


## 2.8.13 (2016-12-28)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.12...2.8.13)

## 2.8.12 (2016-12-26)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.11...2.8.12)
### Fixed
- movie list CLI - Fixed crash. Fixed [#1585](https://github.com/Flexget/Flexget/issues/1585)


## 2.8.11 (2016-12-24)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.10...2.8.11)
### Fixed
- Logger does not attempt to print characters unsupported by current terminal. fix [#1558](https://github.com/Flexget/Flexget/issues/1558)


## 2.8.10 (2016-12-23)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.9...2.8.10)
### Fixed
- Errors with some colorized non-ascii text being sent from daemon on py27 fix [#1553](https://github.com/Flexget/Flexget/issues/1553)
- email - Use `text_to_native_str` to avoid crash on some auth types. Fixes [#1569](https://github.com/Flexget/Flexget/issues/1569)


## 2.8.9 (2016-12-22)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.8...2.8.9)
### Fixed
- failed CLI - Added another column to be wrapped. Fixes [#1580](https://github.com/Flexget/Flexget/issues/1580)


## 2.8.8 (2016-12-20)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.7...2.8.8)
### Added
- New sort_by_weight plugin

### Fixed
- imdb: updated language parsing to search for 'primary_language'


## 2.8.7 (2016-12-19)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.6...2.8.7)
### Added
- movie-list CLI - Added ability to delete movie by ID

### Fixed
- Form plugin not working on pages including non-ascii data. fix [#1576](https://github.com/Flexget/Flexget/issues/1576)


## 2.8.6 (2016-12-18)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.5...2.8.6)
### Fixed
- T411: Update domain url to .li, fixes [#1567](https://github.com/Flexget/Flexget/issues/1567)

### Changed
- trakt_lookup: removed images as Trakt.tv no longer provides them


## 2.8.5 (2016-12-17)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.4...2.8.5)
### Fixed
- Updated horriblesubs to use cfscrape


## 2.8.4 (2016-12-13)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.3...2.8.4)
### Fixed
- Fix flexget-headless crashing on Windows. fix [#1556](https://github.com/Flexget/Flexget/issues/1556)
- Crashes on generating random URLs on Python 3


## 2.8.3 (2016-12-12)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.2...2.8.3)
### Fixed
- changed rss template to use relevant `tvdb_posters` field
- changed html templates to use relevant `tvdb_posters` field. Fixed [#1548](https://github.com/Flexget/Flexget/issues/1548)


## 2.8.2 (2016-12-11)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.1...2.8.2)
### Fixed
- Prevent task_notify from sending notifications when there are no accepted/failed entries.
- rendering a template no longer crashes if entry.task is None, fixes [#1545](https://github.com/Flexget/Flexget/issues/1545)


## 2.8.1 (2016-12-09)
[all commits](https://github.com/Flexget/Flexget/compare/2.8.0...2.8.1)
### Fixed
- Prevent crash in imdb_list when trying to list_match against an entry without imdb_id
- notify - Deprecation notice appeared incorrectly
- pushover - Correctly catch and handle RequestException when its Response is None
- pushbullet - Correctly catch and handle RequestException when its Response is None


## 2.8.0 (2016-12-08)
[all commits](https://github.com/Flexget/Flexget/compare/2.7.4...2.8.0)
### Fixed
- render - Removed string replacement

### Added
- npo_watchlist - Fetch more of the series data exposed by NPO.nl

### Changed
- Notifiers tweaks


## 2.7.4 (2016-12-07)
[all commits](https://github.com/Flexget/Flexget/compare/2.7.3...2.7.4)
### Fixed
- archives plugin: treat IOErrors as “not a directory”. closes [#1525](https://github.com/Flexget/Flexget/issues/1525)
- entry render issue - Correctly create the `task_name` attribute. Fixes [#1540](https://github.com/Flexget/Flexget/issues/1540), Fixes [#1538](https://github.com/Flexget/Flexget/issues/1538)

### Added
- from_deluge - Allow user to specify extra keys wanted to be populated with from_deluge


## 2.7.3 (2016-12-06)
[all commits](https://github.com/Flexget/Flexget/compare/2.7.2...2.7.3)
### Fixed
- apple_trailers: fixed some crashing caused by a typo


## 2.7.2 (2016-12-05)
[all commits](https://github.com/Flexget/Flexget/compare/2.7.1...2.7.2)
### Changed
- api_trakt: now uses the new api url, api.trakt.tv


## 2.7.1 (2016-12-02)
[all commits](https://github.com/Flexget/Flexget/compare/2.7.0...2.7.1)



## 2.7.0 (2016-12-01)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.9...2.7.0)
### Fixed
- couchpotato_list - Fixed crash due to corrupt CP data. Closed [#1444](https://github.com/Flexget/Flexget/issues/1444)

### Added
- join - Added join notifier plugin
- notify_crash - Added notify crash plugin
- notify - Added notify plugin
- Notifier plugin and interface

### Removed
- whatcd - Removed what.cd plugin

### Changed
- All notifier plugins have been completely refactored, schema changes


## 2.6.9 (2016-11-30)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.8...2.6.9)

## 2.6.8 (2016-11-29)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.7...2.6.8)

## 2.6.7 (2016-11-28)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.6...2.6.7)
### Changed
- pending_approval - Changed plugin operation  to a more correct one

### Fixed
- rtorrent: properly use the port from uri, fixes [#1522](https://github.com/Flexget/Flexget/issues/1522)
- terminal - Fixed wrong value check and wrapped TerminalTable in try block for `series show` CLI. Fixed [#1520](https://github.com/Flexget/Flexget/issues/1520)


## 2.6.6 (2016-11-26)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.5...2.6.6)

## 2.6.5 (2016-11-25)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.4...2.6.5)

## 2.6.4 (2016-11-24)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.3...2.6.4)
### Fixed
- terminal_table - Handle scenario that terminal is still too small after dropping and wrapping everything possible
- pending CLI - Fixed crash due to not dropping and/or wrapping correct columns
- terminal - Fixed crash when trying to word wrap a non str value

### Added
- [WebUI] Basic pending page
- pending CLI - Added `clear` action to deleted all pending entries


## 2.6.3 (2016-11-23)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.2...2.6.3)
### Added
- [pending_approval](/Plugins/pending_approval) - Pending approval plugin, CLI & API


## 2.6.2 (2016-11-22)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.1...2.6.2)
### Fixed
- formatdate - Fix format encoding
- require_field - Reject entry if field is None


## 2.6.1 (2016-11-18)
[all commits](https://github.com/Flexget/Flexget/compare/2.6.0...2.6.1)
### Fixed
- fuzer - Fixed file size regex


## 2.6.0 (2016-11-16)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.22...2.6.0)
### Added
- imdb_watchlist - Readded new/old `imdb_watchlist`

### Changed
- [move](/Plugins/move)/[copy](/Plugins/copy) plugins: 
  - Changed option `filename` to `rename` since it caused issues with [filesystem](/Plugins/filesystem) plugin.
  - jinja2 replacement render issues will not abort task and not fallback to default.
- Daemon:
  - `flexget daemon reload` has been renamed to `flexget daemon reload-config` to avoid confusion.
  - `--config-autoreload` action for `flexget daemon start` has been renamed to `--autoreload-config`.
  - `flexget daemon enable-autoreload` and `flexget daemon disable-autoreload` have been removed as their use was limited and ill-conceived.

### Fixed
- crossmatch: no longer tries to match non-existing fields, fixes [#1503](https://github.com/Flexget/Flexget/issues/1503)
- api_tvdb - Language param was not passed to episode lookup


## 2.5.22 (2016-11-14)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.21...2.5.22)
### Fixed
- web server - Config changes now affect web server, no need to restart daemon
- clean_transmission: fixed the preserve tracker matching


## 2.5.21 (2016-11-13)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.20...2.5.21)
### Fixed
- transmission: fixed json decode error in py3, fixes [#1264](https://github.com/Flexget/Flexget/issues/1264)

### Changed
- aria2: no longer requiring that 'path' exists, closes [#1493](https://github.com/Flexget/Flexget/issues/1493)


## 2.5.20 (2016-11-12)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.19...2.5.20)
### Fixed
- clean_transmission: fixed crash when preserve_tracker is not set


## 2.5.19 (2016-11-11)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.18...2.5.19)
### Changed
- rtorrent: added support for Digest auth
- status - Status plugin and UI/API changes

## 2.5.18 (2016-11-10)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.17...2.5.18)
### Fixed
- [WebUI] Fixed 'No metadata found' showing on every series entry

## 2.5.17 (2016-11-09)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.16...2.5.17)
### Added
- exec - Added for_undecided
- transmission - Preserve torrents based on presence of trackers


## 2.5.16 (2016-11-08)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.15...2.5.16)

## 2.5.15 (2016-11-07)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.14...2.5.15)

## 2.5.14 (2016-11-06)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.13...2.5.14)
### Changed
- myepisodes has been refactored


## 2.5.13 (2016-11-05)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.12...2.5.13)

## 2.5.12 (2016-11-04)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.11...2.5.12)
### Added
- [WebUI] Added status page with latest task execution data
- Task Status API - Added include last execution flag
- API - Tasks status API

### Changed
- verify_ssl_certificates: warnings about disabling SSL verification will now be suppressed.


## 2.5.11 (2016-11-03)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.10...2.5.11)
### Fixed
- daemon: Automatically restart task queue if it crashes unexpectedly, related [#1254](https://github.com/Flexget/Flexget/issues/1254)
- Better string encoding in exec plugin. fix [#1295](https://github.com/Flexget/Flexget/issues/1295)
- rarbg - Set default language to 'en' when using thetvdb_lookup from rarbg. Closes [#1481](https://github.com/Flexget/Flexget/issues/1481)
- UI/API - Added relevant response header for correct etag generation


## 2.5.10 (2016-11-02)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.9...2.5.10)
### Changed
- api_tmdb - TMDB API fixes and changes

### Fixed
- api_bluray: (hopefully) fixed crashing when turning request into json, closes [#1479](https://github.com/Flexget/Flexget/issues/1479)


## 2.5.9 (2016-11-01)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.8...2.5.9)
### Added
- API - Added IRC endpoint and minor changes to CLI


## 2.5.8 (2016-10-31)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.7...2.5.8)
### Added
- pushover - Added html support, notification limit support and slightly more detailed logs

### Fixed
- irc: fixed crash when it cannot locate tracker file on github


## 2.5.7 (2016-10-30)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.6...2.5.7)
### Fixed
- guessit: suppress encoding errors caused by guessit and rebulk not handling unicode properly, related [#1298](https://github.com/Flexget/Flexget/issues/1298)
- pogcal_acquired: updated to new login url and fixed some soup, fixes [#1245](https://github.com/Flexget/Flexget/issues/1245)
- pogcal: include url in entry


## 2.5.6 (2016-10-29)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.5...2.5.6)
### Fixed
- discover: fixed a logging error where a wrong number of arguments were given, fixes [#1471](https://github.com/Flexget/Flexget/issues/1471)


## 2.5.5 (2016-10-28)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.4...2.5.5)
### Fixed
- torrent_alive: returns 0 if html is received, fixes [#1434](https://github.com/Flexget/Flexget/issues/1434)
- series CLI - Made series show download index visible with porcelain mode

### Changed
- [WebUI] Movies metadata is now fetched from TMDB instead of Trakt
- seen cli - Made cli search parse IMDB ID like seen add. Closes [#1427](https://github.com/Flexget/Flexget/issues/1427)

### Added
- [WebUI] Added database operations as a right side menu with different options


## 2.5.4 (2016-10-27)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.3...2.5.4)
### Fixed
- npo_watchlist - Added request error catching. Closes [#1462](https://github.com/Flexget/Flexget/issues/1462)
- api_tvdb - Improved logic for series that return with no title. Closed [#1466](https://github.com/Flexget/Flexget/issues/1466)
- web server - Updated import to match flask-login changes, updated requirement. Closed [#1467](https://github.com/Flexget/Flexget/issues/1467)
- web_server: temporarily locked flask-login to 0.3.2, related [#1467](https://github.com/Flexget/Flexget/issues/1467)
- Trakt lookup expired movie, returns trakt_released field now as Date field, same as when returned from database


## 2.5.3 (2016-10-26)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.2...2.5.3)
### Added
- Entry List - Entry list now merges all saved data on match

### Fixed
- tmdb_lookup: no longer crashes when release date is empty, fixes [#1456](https://github.com/Flexget/Flexget/issues/1456)
- seen CLI - Readded seen add method. Closes [#1463](https://github.com/Flexget/Flexget/issues/1463)


## 2.5.2 (2016-10-25)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.1...2.5.2)

## 2.5.1 (2016-10-23)
[all commits](https://github.com/Flexget/Flexget/compare/2.5.0...2.5.1)
### Changed
- daemon: no longer automatically reloads config, can be enabled with `--config-autoreload` or new cli commands
- simplified `irc status`


## 2.5.0 (2016-10-22)
[all commits](https://github.com/Flexget/Flexget/compare/2.4.2...2.5.0)
### Fixed
- Fix CLI table and color behavior when a daemon is running. fix [#1457](https://github.com/Flexget/Flexget/issues/1457)


## 2.4.2 (2016-10-21)
[all commits](https://github.com/Flexget/Flexget/compare/2.4.1...2.4.2)
### Fixed
- terminal - Fixed colorization when piping. Closes [#1361](https://github.com/Flexget/Flexget/issues/1361)

### Added
- API - TMDB lookup API
- thetvdb_lookup - Added languages lookup support. Closes [#1453](https://github.com/Flexget/Flexget/issues/1453)

### Changed
- [WebUI]Schedules gracefully handles disabled scheduler
- [WebUI] Series page gracefully handles failure to get metadata


## 2.4.1 (2016-10-20)
[all commits](https://github.com/Flexget/Flexget/compare/2.4.0...2.4.1)
### Changed
- terminal - Force table type to be ASCII and remove all colors when not TTY. Related [#1223](https://github.com/Flexget/Flexget/issues/1223), Fixes [#1407](https://github.com/Flexget/Flexget/issues/1407)

### Fixed
- [Webui] Execute page now sorts the tasks by priority when streaming, preventing results from being added to another task

### Added
- [Webui] History and series pages now have sorting possibility
- corssmatch - Update Crossmatch with Exact (yes/no) search option
- nfo_lookup plugin - Get metadata from nfo file to aid IMDB search


## 2.4.0 (2016-10-19)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.46...2.4.0)
### Fixed
- [WebUI] Config editor regains focus after closing successful update dialog, fixes [#1451](https://github.com/Flexget/Flexget/issues/1451)
- movie list API - Changed logic to slice after sorting. Fixes [#1347](https://github.com/Flexget/Flexget/issues/1347)
- csv: no longer crashes in Python 3

### Changed
- Daemon will now auto-reload config file if it changes
- tmdb_released has been changed to a Date
- move/copy/delete: 'along' has been simplified and will pick all sibling files that are similar in name with the specified extensions
- API refactor


## 2.3.46 (2016-10-17)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.45...2.3.46)
### Fixed
- download: no longer crashes on permission errors, related [#1448](https://github.com/Flexget/Flexget/issues/1448)


## 2.3.45 (2016-10-16)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.44...2.3.45)
### Changed
- irc daemon: handle simultaneous announcements


## 2.3.44 (2016-10-13)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.43...2.3.44)
### Fixed
- piratebay: support size unit of "B"
- --debug-db: now supports SQLAlchemy 1.1.1+, fixes [#1439](https://github.com/Flexget/Flexget/issues/1439)
- pushbullet: properly format the api key in Python 3.4, fixes [#1445](https://github.com/Flexget/Flexget/issues/1445)
- internal series parser: SSEE format changes, eg. 1001 will be parsed as S10E01 if identified_by: ep is enabled


## 2.3.43 (2016-10-11)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.42...2.3.43)

## 2.3.42 (2016-10-08)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.41...2.3.42)
### Fixed
- irc daemon: no longer crashes when trying to url quote unicode


## 2.3.41 (2016-10-04)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.40...2.3.41)
### Fixed
- tvmaze: bad episode data no longer causes a crash due to MultipleResultsFound, fixes [#1433](https://github.com/Flexget/Flexget/issues/1433)


## 2.3.40 (2016-10-03)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.39...2.3.40)

## 2.3.39 (2016-09-30)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.38...2.3.39)
### Fixed
- WebUI - Fixed UI constantly called /server/version endpoint when navigating
- No longer crashes when checking for config modification on reruns


## 2.3.38 (2016-09-29)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.37...2.3.38)
### Changed
- bluray: no longer looks for release dates if movie_year is greater than current year
- regexp-list cli: default list is now "regexps" if no list is specified

### Fixed
- alpharatio: updated to new layout, fixes [#1420](https://github.com/Flexget/Flexget/issues/1420)


## 2.3.37 (2016-09-28)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.36...2.3.37)
### Fixed
- next_sonarr_episodes - Forgot to format string correctly. Closes [#1425](https://github.com/Flexget/Flexget/issues/1425)


## 2.3.36 (2016-09-27)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.35...2.3.36)
### Fixed
- rarbg: No longer converts search strings to bytes, fixes [#1251](https://github.com/Flexget/Flexget/issues/1251)
- manager - Revert changes that allow daemon to reload config as it was causing issues. Fixes [#1422](https://github.com/Flexget/Flexget/issues/1422) . Related to [#1299](https://github.com/Flexget/Flexget/issues/1299) ,[#1300](https://github.com/Flexget/Flexget/issues/1300)
- rtorrent: magnet uris are now passed properly as bytes, fixes [#1328](https://github.com/Flexget/Flexget/issues/1328)
- api_trakt: no longer crashes when a lookup returns no genres

### Changed
- WebUI - Deleting Seen Entry now requires confirmation


## 2.3.35 (2016-09-26)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.34...2.3.35)
### Fixed
- bumped the required python-dateutil version since 2.5.2 contains a bug in the date parser, fixes [#1393](https://github.com/Flexget/Flexget/issues/1393)
- thetvdb_lookup: workaround for the language error that sometimes happens, fixes [#1424](https://github.com/Flexget/Flexget/issues/1424)
- file size parsing now supports decimal separators, fixes [#1423](https://github.com/Flexget/Flexget/issues/1423)


## 2.3.34 (2016-09-25)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.33...2.3.34)
### Changed
- configure_series - Made `from` into a required schema property

### Fixed
- serienjunkies: no longer crashes when parsing language, fixes [#1409](https://github.com/Flexget/Flexget/issues/1409)
- movie list CLI - Fixed crash on generating new movie list on the fly
- proper_movies, exists_movie: now uses movie year when searching, fixes [#1351](https://github.com/Flexget/Flexget/issues/1351)
- imdb_lookup: imdb_languages field is now populated correctly


## 2.3.33 (2016-09-23)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.32...2.3.33)
### Added
- WebUI - add new movies, title now links to IMDB
- WebUI - search term to add a movie can now be cleared easily

### Fixed
- Prevent metainfo_content_size from crashing with an empty location. fix [#1403](https://github.com/Flexget/Flexget/issues/1403)
- Changed status to use local time, some mismatch with history will occur

### Changed
- WebUI - Execute results show a different icon for accepted/undecided results


## 2.3.32 (2016-09-21)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.31...2.3.32)
### Added
- WebUI - Seen entries can now be removed
- WebUi - History can now be filtered based on task name

### Changed
- web_server - Removed pyopenssl dep, use builtin cherrypy. Fixes [#1414](https://github.com/Flexget/Flexget/issues/1414)

### Fixed
- configure_series: Fixed SAWarning


## 2.3.31 (2016-09-20)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.30...2.3.31)
### Added
- Add ssl support to webserver

### Fixed
- Failing UI tests should work again

### Changed
- WebUI - New version available icon changed to question mark, as to not confuse users to be able to update using it


## 2.3.30 (2016-09-20)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.29...2.3.30)
### Changed
- Webui - Update available icon now links to Flexget's ChangeLog


## 2.3.29 (2016-09-19)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.28...2.3.29)
### Changed
- cached api - More detailed error responses. Related [#1410](https://github.com/Flexget/Flexget/issues/1410)

### Fixed
- cached api - Using config base dir instead of working dir. Fixes [#1410](https://github.com/Flexget/Flexget/issues/1410)
- daemon: reloading config now properly triggers a config change in tasks, fixes [#1406](https://github.com/Flexget/Flexget/issues/1406)

### Added
- irc: reloading config will only restart irc connections that contain changes


## 2.3.28 (2016-09-17)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.27...2.3.28)
### Added
- Movies can now be added to a list in the WebUI ([#1364](https://github.com/Flexget/Flexget/issues/1364))


## 2.3.27 (2016-09-15)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.26...2.3.27)
### Added
- [WebUI] Checking of actual semver, not just lazy comparison of strings
- version info is now shown in UI, icon is shown when new version is available (currently only does lazy string comparison, will change to actual semver check later)

### Fixed
- Adding new series and next_series_episodes workaround
- daemon: no longer crashes on older python 2.7, fixes [#1405](https://github.com/Flexget/Flexget/issues/1405)


## 2.3.26 (2016-09-13)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.25...2.3.26)
### Fixed
- Unknown options to flexget CLI commands now cause errors and show help. fix [#1404](https://github.com/Flexget/Flexget/issues/1404)
- pyload: no longer inexplicably throws error 91, fixes [#1136](https://github.com/Flexget/Flexget/issues/1136)


## 2.3.25 (2016-09-12)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.24...2.3.25)
### Fixed
- telegram - Fixed telegram parsing fallback. Closes [#1385](https://github.com/Flexget/Flexget/issues/1385)


## 2.3.24 (2016-09-11)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.23...2.3.24)
### Changed
- entry list cli - URL will be used and not original URL by default when adding new entry

### Added
- trakt_lookup: will now also add user ratings for season, series, ep and movies


## 2.3.23 (2016-09-10)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.22...2.3.23)
### Changed
- npo_watchlist: Rewrite, after big changes to npo.nl


## 2.3.22 (2016-09-09)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.21...2.3.22)
### Changed
- qbittorrent: Send torrent file instead of url if possible, fixes [#1390](https://github.com/Flexget/Flexget/issues/1390)

### Added
- convert_magnet: new plugin for converting magnets to torrents using libtorrent

### Fixed
- download: fix error handling in py3


## 2.3.21 (2016-09-08)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.20...2.3.21)
### Added
- server api - Added latest flexget version to response


## 2.3.20 (2016-09-08)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.19...2.3.20)

## 2.3.19 (2016-09-07)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.18...2.3.19)

### Added
- Revert " server api - Added latest flexget version to `/version/` endpoint"


## 2.3.18 (2016-09-05)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.17...2.3.18)
### Fixed
- cached api - Fixed ApiError format
- trakt: no longer crashes because of a database error, see [#1191](https://github.com/Flexget/Flexget/issues/1191)


## 2.3.17 (2016-09-04)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.16...2.3.17)
### Fixed
- subtitle_list: will no longer spit out directories when used as input
- subtitle_list: fixed recursion depth=1 such that it does no recursion

### Added
- Created cached endpoint and util
- subtitle_list: added validation to recursion_depth. Must be greater than 0.
- subliminal: added test mode so subtitles are not downloaded with --test


## 2.3.16 (2016-09-01)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.15...2.3.16)
### Changed
- [WebUI] Movies are now sorted from A-Z
- [WebUI] Series are now sorted from A-Z


## 2.3.15 (2016-08-31)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.14...2.3.15)
### Fixed
- trakt_list: Adding episodes to a trakt list no longer requires a lookup


## 2.3.14 (2016-08-30)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.13...2.3.14)
### Added
- reorder_quality plugin

### Fixed
- retry_failed could cause crash by datetime overflow, cap retry to 30 days

### Changed
- Symlink plugin can now be se to ignore existing links instead of failing


## 2.3.13 (2016-08-29)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.12...2.3.13)
### Fixed
- max_reruns: will now set the old max reruns value properly after task execution
- Command history with --short no longer leaves out last item
- regexp_list: fixed delete on list_match not working

### Changed
- run_task: Changed schema to allow multiple tasks and fixed some bugs
- rarbg: will no longer log error when imdb id is not found when searching


## 2.3.12 (2016-08-28)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.11...2.3.12)
### Fixed
- series cli - Added check for existence of table parser. Fixes [#1378](https://github.com/Flexget/Flexget/issues/1378)
- seen cli - Fix crash on no table data. Fixes [#1373](https://github.com/Flexget/Flexget/issues/1373)
- fuzer - Raise plugin error in case main results table could not be found.

### Added
- New categories in RarBG search plugin
- New AlphaRatio search plugin

### Changed
- trakt_list: better error message when trying to use episodes type for collection list, closes [#1380](https://github.com/Flexget/Flexget/issues/1380)
- movie parser: Improved year and propers parsing


## 2.3.11 (2016-08-27)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.10...2.3.11)
### Fixed
- piratebay: No longer crashes because of unexpected html tags, fixes [#1359](https://github.com/Flexget/Flexget/issues/1359)


## 2.3.10 (2016-08-27)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.9...2.3.10)
### Fixed
- regexp_list: list and purge no longer crash on non-existing lists


## 2.3.9 (2016-08-26)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.8...2.3.9)
### Fixed
- Table width on command `failed`

### Added
- regexp_list: added cli commands


## 2.3.8 (2016-08-25)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.7...2.3.8)
### Fixed
- [WebUI] Fixed confirmation dialogs, they now correctly show the content again
- terminal - Correctly remove colors on porcelain and on no TTY. Fixes [#1361](https://github.com/Flexget/Flexget/issues/1361)


## 2.3.7 (2016-08-25)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.6...2.3.7)
### Fixed
- api_bluray: no longer crashes when movie contains very little information, fixes [#1353](https://github.com/Flexget/Flexget/issues/1353)
- iptorrents - Fix plugin iptorrents, fixes [#1368](https://github.com/Flexget/Flexget/issues/1368)


## 2.3.6 (2016-08-24)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.5...2.3.6)
### Fixed
- myepiaodes - Adjust myepisodes to new tvdb plugin api
- movie list CLI - Fixed crash when adding to new list
- Restored seen search fields. [#1362](https://github.com/Flexget/Flexget/issues/1362)

### Added
- IMDB Search API


## 2.3.5 (2016-08-23)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.4...2.3.5)
### Fixed
- seen cli - Added missing fields. Fixes [#1362](https://github.com/Flexget/Flexget/issues/1362)
- movie list API - Fixed crash when not sending identifiers key. Fixes [#1363](https://github.com/Flexget/Flexget/issues/1363)
- api_tvmaze - Broader exception handling
- morethantv: content_size is now properly set in entries

### Added
- imdb list - Added support for video game format. Closed [#1355](https://github.com/Flexget/Flexget/issues/1355)


## 2.3.4 (2016-08-21)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.3...2.3.4)
### Fixed
- search plugins: no longer crashes on single digit sizes eg. "1 GiB", fixes [#1359](https://github.com/Flexget/Flexget/issues/1359)
- irc: cli `status all` now only prints once

### Added
- re-added rutracker plugin


## 2.3.3 (2016-08-20)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.2...2.3.3)
### Added
- irc: added CLI commands for restarting, stopping and checking irc connections


## 2.3.2 (2016-08-19)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.1...2.3.2)
### Fixed
- irc: putting ~ (tilde) in tracker config path no longer fails to find it on disk
- irc: specifying tracker file by name only will no longer fail to find it on disk


## 2.3.1 (2016-08-18)
[all commits](https://github.com/Flexget/Flexget/compare/2.3.0...2.3.1)
### Fixed
- series: Fix crash when using guessit parser on shows with 'Part X' identifiers. fix [#1326](https://github.com/Flexget/Flexget/issues/1326)
- aria2 won't crash on jinja2 render errors
- Make aria2 respect --test mode again.
- aria2 - Fix aria2 plugin on python 3.
- piratebay entry size is now parsed correctly
- api_bluray: bluray lookup and estimator no longer crash when info not found, fixes [#1352](https://github.com/Flexget/Flexget/issues/1352) [#1353](https://github.com/Flexget/Flexget/issues/1353)
- [WebUI] Locked all bower deps to patch level. fixes [#1350](https://github.com/Flexget/Flexget/issues/1350)


## 2.3.0 (2016-08-17)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.22...2.3.0)
### Fixed
- fixed square brackets messing up move's along, fixes [#1348](https://github.com/Flexget/Flexget/issues/1348)
- IMDB List - Added more supported types. Fixes [#1343](https://github.com/Flexget/Flexget/issues/1343)

### Changed
- webrip is now considered better than screeners
- Many CLI commands now have nice formatted table output
- CLI command `flexget trakt show` has been renamed to `flexget trakt list`
- discover `release_estimations` now defaults to `strict` meaning anything with no release date or one that lies in the future will not be included in the search
- discover will now keep searching for new episodes until it fails to find any (maximum 100 runs). Can be set to the old behaviour with `max_reruns` plugin.
- [Aria2](/Plugins/aria2) is drastically simplified and many features are removed.

### Removed
- Removed `movie_queue` and all related plugins.
- Removed `imdb_required` plugin, switch to `imdb_lookup` and `require_field`
- Removed `subtitle_queue` plugin
- Removed `rutracker`  plugin
- Removed `torrentz` plugin
- Removed `newzleech` plugin
- Removed `publichd` plugin
- Removed `bt-chat` plugin
- Removed `btjunkie` plugin
- Removed `isohunt` plugin
- Removed `redskunk` plugin
- Removed `stmusic` plugin

### Added
- added blu-ray.com movie estimator (takes priority over the old one)
- blu-ray.com lookup (`bluray_lookup`)


## 2.2.22 (2016-08-17)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.21...2.2.22)
### Fixed
- html plugin will now properly dump the contents if configured to
- form - Solved TypeError Issue. Fixes [#1344](https://github.com/Flexget/Flexget/issues/1344)


## 2.2.21 (2016-08-16)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.20...2.2.21)
### Fixed
- IMDB list - Added `documentary` type to be parsed as movie. Fixes [#1343](https://github.com/Flexget/Flexget/issues/1343)
- Fuzer - Fixed updated site layout


## 2.2.20 (2016-08-15)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.19...2.2.20)

## 2.2.19 (2016-08-14)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.18...2.2.19)
### Changed
- Allow use of `now` in email plugin templates. fix [#1335](https://github.com/Flexget/Flexget/issues/1335)


## 2.2.18 (2016-08-14)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.17...2.2.18)
### Fixed
- imdb list - Correction IMDb login fixes [#1321](https://github.com/Flexget/Flexget/issues/1321)


## 2.2.17 (2016-08-12)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.16...2.2.17)
### Fixed
- irc: Fixed unicode errors when reading tracker file
- irc: Fixed KeyError when extracting tags from announcement

### Changed
- irc: tracker_file option is no longer case sensitive nor does it require .tracker extension


## 2.2.16 (2016-08-11)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.15...2.2.16)
### Added
- Plex - Added two new fields


## 2.2.15 (2016-08-10)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.14...2.2.15)
### Fixed
- Pushbullet: Fixed api key being invalid in Py3, fixes [#1320](https://github.com/Flexget/Flexget/issues/1320)


## 2.2.14 (2016-08-09)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.13...2.2.14)
### Fixed
- tvmaze and tmdb caches are no longer cleared on each run


## 2.2.13 (2016-08-09)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.12...2.2.13)
### Fixed
- Fixed crash in trakt plugins with latest version of requests library.


## 2.2.12 (2016-08-08)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.11...2.2.12)

## 2.2.11 (2016-08-07)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.10...2.2.11)
### Fixed
- move - 'files' and 'subdirs' no longer crash on single strings
- html - fixed regular expr used to create title from url, really fixes [#1250](https://github.com/Flexget/Flexget/issues/1250)

### Changed
- Subliminal plugin now finds embedded subtitles (again). Also fixed single mode when found language is undefined.

### Added
- Prowl - Allow the sending of the prowl url parameter


## 2.2.10 (2016-08-07)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.9...2.2.10)
### Added
- Plex - Populate series info for Plex episodes


## 2.2.9 (2016-08-05)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.8...2.2.9)
### Fixed
- Html plugin can create titles from magnet links again. fixes [#1250](https://github.com/Flexget/Flexget/issues/1250)


## 2.2.8 (2016-08-04)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.7...2.2.8)

## 2.2.7 (2016-08-03)
[all commits](https://github.com/Flexget/Flexget/compare/2.2.6...2.2.7)

## 2.2.6 (2016-08-03)
[all commits](https://github.com/Flexget/Flexget/compare/1501a7d622a3fff4dd9588cda8e15dfe770791b6...0d110294637c5edd42dbf63179b3595dfa8e43c2)

## 2.2.5 (2016-08-02)
[all commits](https://github.com/Flexget/Flexget/compare/c79e6c077a76bf810ccbdb2715c92cfa86064248...1501a7d622a3fff4dd9588cda8e15dfe770791b6)
### Fixed
- Requrie a version of Beautifulsoup4 that can handle different html5lib versions. fix [#1309](https://github.com/Flexget/Flexget/issues/1309)


## 2.2.4 (2016-08-01)
[all commits](https://github.com/Flexget/Flexget/compare/7926bcc5da24cbbe9e689c19a940aa3862aca7be...c79e6c077a76bf810ccbdb2715c92cfa86064248)
### Fixed
- 'local' is now strictly a boolean


## 2.2.3 (2016-07-31)
[all commits](https://github.com/Flexget/Flexget/compare/426fe0bf6611fc4fde00db0687ec33708943808c...7926bcc5da24cbbe9e689c19a940aa3862aca7be)
### Fixed
- tvmaze_api - Removed searching from cache via airdate. Fixes [#1305](https://github.com/Flexget/Flexget/issues/1305)


## 2.2.2 (2016-07-29)
[all commits](https://github.com/Flexget/Flexget/compare/19f63cfabcf1b7d877661841539dac642784792e...426fe0bf6611fc4fde00db0687ec33708943808c)

## 2.2.1 (2016-07-28)
[all commits](https://github.com/Flexget/Flexget/compare/986aa70f9bc80209adc796ec14a3a0730baa6ef0...19f63cfabcf1b7d877661841539dac642784792e)

## 2.2.0 (2016-07-27)
[all commits](https://github.com/Flexget/Flexget/compare/ef190de036680eee0826abe4c1604e37676e3f86...986aa70f9bc80209adc796ec14a3a0730baa6ef0)
### Fixed
- require_field - Improve check logic.
- require_field - Do not implicitly convert to bool.

### Changed
- move/copy/delete 'along' now supports subdirs


## 2.1.25 (2016-07-26)
[all commits](https://github.com/Flexget/Flexget/compare/9342a97dd33817bde8036fa033bcf92f5affbaa7...ef190de036680eee0826abe4c1604e37676e3f86)
### Fixed
- [WebUI] Series episodes block incorrectly cutting of series row
- list match - Tighter schema
- **plugins API** - Makes args case insensitive


## 2.1.24 (2016-07-25)
[all commits](https://github.com/Flexget/Flexget/compare/ff7845498973ad60e44ea1ced9f1c406d050d4d8...9342a97dd33817bde8036fa033bcf92f5affbaa7)
### Fixed
- **fuzer** - Did not return results correctly


## 2.1.23 (2016-07-24)
[all commits](https://github.com/Flexget/Flexget/compare/a95e40937a4d5a5efce0302fb04d671d27cb832f...ff7845498973ad60e44ea1ced9f1c406d050d4d8)
### Fixed
- Make tail plugin work consistenly with unicode on py2/3. fix [#1269](https://github.com/Flexget/Flexget/issues/1269)
- telegram - Changed plugin to be an output plugin and not an exit plugin
- database API - Fixed return object to be a list

### Changed
- Tail plugin defaults to utf8 instead of ascii encoding


## 2.1.22 (2016-07-23)
[all commits](https://github.com/Flexget/Flexget/compare/ae8ef4e20e36b90ca2896bdc123ebb09f89f0a88...a95e40937a4d5a5efce0302fb04d671d27cb832f)

## 2.1.21 (2016-07-23)
[all commits](https://github.com/Flexget/Flexget/compare/69f3550e7fd600727150e32f63f004d7c590b458...ae8ef4e20e36b90ca2896bdc123ebb09f89f0a88)
### Fixed
- changed pushbullet error logging, fixes [#1225](https://github.com/Flexget/Flexget/issues/1225)
- irc will now properly try to reconnect again
- IMDB list - Correctly set type for different IMDB entities. Fixes [#1270](https://github.com/Flexget/Flexget/issues/1270)
- clean_source now uses old location, fixes  [#1284](https://github.com/Flexget/Flexget/issues/1284)
- Stricter episode matching, finally fixes [#1111](https://github.com/Flexget/Flexget/issues/1111)
- thetvdb_favorites deprecation message no longer shows for thetvdb_list
- fuzer - Changed logic to use the new search API

### Changed
- added web quality, closes [#1218](https://github.com/Flexget/Flexget/issues/1218)
- fuzer -Refactor and added support for search via imdb_id


## 2.1.20 (2016-07-22)
[all commits](https://github.com/Flexget/Flexget/compare/c6cd875e4f2a686266ab3f254cb55ab12801d3ba...69f3550e7fd600727150e32f63f004d7c590b458)
### Fixed
- changed pushbullet error logging, fixes [#1225](https://github.com/Flexget/Flexget/issues/1225)
- irc will now properly try to reconnect again
- manual plugin - Manual plugin never aborted any task. Fixes [#1291](https://github.com/Flexget/Flexget/issues/1291)

### Changed
- added web quality, closes [#1218](https://github.com/Flexget/Flexget/issues/1218)


## 2.1.19 (2016-07-21)
[all commits](https://github.com/Flexget/Flexget/compare/0c951c0d5630c2450151d371265599c5e89990c7...c6cd875e4f2a686266ab3f254cb55ab12801d3ba)

## 2.1.18 (2016-07-20)
[all commits](https://github.com/Flexget/Flexget/compare/da6f88c37348b48879ff84679cb93e72185a0d0c...0c951c0d5630c2450151d371265599c5e89990c7)

## 2.1.17 (2016-07-19)
[all commits](https://github.com/Flexget/Flexget/compare/d0cb205a7e1cb370bb897a73c4855231e8d609c3...da6f88c37348b48879ff84679cb93e72185a0d0c)
### Fixed
- IMDB list - Correctly set type for different IMDB entities. Fixes [#1270](https://github.com/Flexget/Flexget/issues/1270)
- clean_source now uses old location, fixes  [#1284](https://github.com/Flexget/Flexget/issues/1284)


## 2.1.16 (2016-07-18)
[all commits](https://github.com/Flexget/Flexget/compare/79b16409667d233f4abb9a65496602759156031e...d0cb205a7e1cb370bb897a73c4855231e8d609c3)
### Changed
- fuzer -Refactor and added support for search via imdb_id

### Fixed
- Stricter episode matching, finally fixes [#1111](https://github.com/Flexget/Flexget/issues/1111)


## 2.1.15 (2016-07-17)
[all commits](https://github.com/Flexget/Flexget/compare/481ddcd11c9707656b013191cb0eb1c39c90d43b...79b16409667d233f4abb9a65496602759156031e)
### Fixed
- thetvdb_favorites deprecation message no longer shows for thetvdb_list
- fuzer - Changed logic to use the new search API
- fuzer - Fixed incorrect search pattern

### Changed
- Allow manipulate to run in modify phase
- Allow setting filename with config in download plugin


## 2.1.14 (2016-07-17)
[all commits](https://github.com/Flexget/Flexget/compare/da203f0bf763280d8555e06270dd70ef965034ef...481ddcd11c9707656b013191cb0eb1c39c90d43b)
### Changed
- only join chan on invite if it's in the list


## 2.1.13 (2016-07-15)
[all commits](https://github.com/Flexget/Flexget/compare/2bbda3456e5e8aff3cefa2c4f988017ca24a52cd...da203f0bf763280d8555e06270dd70ef965034ef)
### Fixed
- Pin html5lib version to prevent bs4 bug.


## 2.1.12 (2016-07-14)
[all commits](https://github.com/Flexget/Flexget/compare/409b4b193182f4d0330d055e8399e69ea6868af8...2bbda3456e5e8aff3cefa2c4f988017ca24a52cd)
### Changed
- no more log "spam", rip decorator


## 2.1.11 (2016-07-13)
[all commits](https://github.com/Flexget/Flexget/compare/9550514bc323c92dfe171e60588e80281223f77d...409b4b193182f4d0330d055e8399e69ea6868af8)
### Fixed
- irc plugin will not try to hash an empty config, fixes [#1274](https://github.com/Flexget/Flexget/issues/1274)
- operation did not complete read fixed


## 2.1.10 (2016-07-13)
[all commits](https://github.com/Flexget/Flexget/compare/aa7f859d1dc20bee818250f38059fe63d24de73f...9550514bc323c92dfe171e60588e80281223f77d)

## 2.1.9 (2016-07-11)
[all commits](https://github.com/Flexget/Flexget/compare/908866d0271d3d3a62007875c67746b1a882a415...aa7f859d1dc20bee818250f38059fe63d24de73f)
### Fixed
- Fuzer Encode password before hashing

### Changed
- download and move now set 'location' field


## 2.1.8 (2016-07-11)
[all commits](https://github.com/Flexget/Flexget/compare/47227877cb277bdcd2bd0f53a88f07b5116faa78...908866d0271d3d3a62007875c67746b1a882a415)

## 2.1.7 (2016-07-07)
[all commits](https://github.com/Flexget/Flexget/compare/9f55caa5fb82090fa362175cfb09e4fd89444e9a...47227877cb277bdcd2bd0f53a88f07b5116faa78)
### Added
- qbittorent - Added ability to not fail html content links

### Fixed
- tvdb - TVDB lookup did not correctly lookup specials.
- tail - Open file as binary. Fixes [#1269](https://github.com/Flexget/Flexget/issues/1269)


## 2.1.6 (2016-07-04)
[all commits](https://github.com/Flexget/Flexget/compare/0d0c20399132d147c586060b9d67cc37102b949c...9f55caa5fb82090fa362175cfb09e4fd89444e9a)
### Fixed
- movie list - explicitly check for movie year. Fixes [#1266](https://github.com/Flexget/Flexget/issues/1266)


## 2.1.5 (2016-07-04)
[all commits](https://github.com/Flexget/Flexget/compare/73b1bf8c9077de0195b12896e20a94949283056d...0d0c20399132d147c586060b9d67cc37102b949c)
### Fixed
- api - Added missing swagger error schema doc for py3
- execute api - Fixed no_cache attribute not stored as expected
- telegram - Fixed telegram error import. Fixes [#1262](https://github.com/Flexget/Flexget/issues/1262)

### Added
- kat - Added anime category


## 2.1.4 (2016-06-29)
[all commits](https://github.com/Flexget/Flexget/compare/4730666e772c0be37a3035f03a208c8df31ff265...73b1bf8c9077de0195b12896e20a94949283056d)

## 2.1.3 (2016-06-28)
[all commits](https://github.com/Flexget/Flexget/compare/a7c6ff200ccb235621994e498f772b443320a506...4730666e772c0be37a3035f03a208c8df31ff265)
### Fixed
- tl - Catch request errors


## 2.1.2 (2016-06-28)
[all commits](https://github.com/Flexget/Flexget/compare/b96962025006ed2a1c6732f0e384d626d1e808ea...a7c6ff200ccb235621994e498f772b443320a506)
### Changed
- allow_dir is only used when adding to the subtitle list

### Fixed
- raw_config - Made endpoint much more robust


## 2.1.1 (2016-06-24)
[all commits](https://github.com/Flexget/Flexget/compare/c76026cdf6b62a8ba326f65496b80788fd34bb84...b96962025006ed2a1c6732f0e384d626d1e808ea)

## 2.1.0 (2016-06-23)
[all commits](https://github.com/Flexget/Flexget/compare/8650012fc0b8aa04756090a01ed86edb6448a90c...c76026cdf6b62a8ba326f65496b80788fd34bb84)
### Fixed
- raw_config API - Fixed py3 compatibility
- API - Response description cannot be null, default is now `Success`. Fixes [#1182](https://github.com/Flexget/Flexget/issues/1182)


## 2.0.51 (2016-06-22)
[all commits](https://github.com/Flexget/Flexget/compare/1727d5618aac4606d506963e78efdd6ee74f2e94...8650012fc0b8aa04756090a01ed86edb6448a90c)
### Fixed
- fixed bad if-statement regarding trakt_released, fixes [#1236](https://github.com/Flexget/Flexget/issues/1236)


## 2.0.50 (2016-06-22)
[all commits](https://github.com/Flexget/Flexget/compare/4aa58b8fb2dfe28239834b035da973a695d68ed0...1727d5618aac4606d506963e78efdd6ee74f2e94)
### Fixed
- Force empty list instead of None in genres and translations, fixes [#1219](https://github.com/Flexget/Flexget/issues/1219)

### Added
- server/raw_config - Added raw config endpoint


## 2.0.49 (2016-06-20)
[all commits](https://github.com/Flexget/Flexget/compare/a786a62de34487bf771d20111ca342170b966473...4aa58b8fb2dfe28239834b035da973a695d68ed0)
### Fixed
- transmission plugin on python 2 with non-ascii paths fix [#1237](https://github.com/Flexget/Flexget/issues/1237)


## 2.0.48 (2016-06-16)
[all commits](https://github.com/Flexget/Flexget/compare/a06552448280d146842b51d82dadad9004eaa2b5...a786a62de34487bf771d20111ca342170b966473)
### Changed
- trakt lookup - Changed some trakt lookup fields to correctly reflect data
- movie list - Added ability for movie list to parse movie title if no identifiers were present

### Added
- added some requested features to subtitle_list, closes [#1224](https://github.com/Flexget/Flexget/issues/1224)


## 2.0.47 (2016-06-16)
[all commits](https://github.com/Flexget/Flexget/compare/dbc2d97f5268b2170a5b55694d3035304b616258...a06552448280d146842b51d82dadad9004eaa2b5)
### Fixed
- entry list CLI - Made entry list CLI syntax consistent with movie list CLI

### Added
- metainfo_movie - Added metainfo_movie plugin


## 2.0.46 (2016-06-14)
[all commits](https://github.com/Flexget/Flexget/compare/3edeedd2a5e3dc1a6a34415c56afc040c768d2bb...dbc2d97f5268b2170a5b55694d3035304b616258)
### Fixed
- newznab - Correctly search for series name. Fixes [#1217](https://github.com/Flexget/Flexget/issues/1217)
- API - Custom JSON formats and blank payload passed non serializable error messages. Fixes [#1235](https://github.com/Flexget/Flexget/issues/1235)


## 2.0.45 (2016-06-14)
[all commits](https://github.com/Flexget/Flexget/compare/0ffe9ffbc71cedb589569e95b631a8ea6874d731...3edeedd2a5e3dc1a6a34415c56afc040c768d2bb)

## 2.0.44 (2016-06-13)
[all commits](https://github.com/Flexget/Flexget/compare/95461c2a8ebff6d65e5846df9872d1274eb66cac...0ffe9ffbc71cedb589569e95b631a8ea6874d731)
### Added
- movie list - Added `added` attribute to movie entry


## 2.0.43 (2016-06-13)
[all commits](https://github.com/Flexget/Flexget/compare/275a162ef94e227f7dac70425b73a0113b0a3219...95461c2a8ebff6d65e5846df9872d1274eb66cac)
### Fixed
- fix pushbullet crash on python 3 fix [#1225](https://github.com/Flexget/Flexget/issues/1225)
- crash with html input plugin when generating titles from url. fix [#1227](https://github.com/Flexget/Flexget/issues/1227)
- Transmission plugin now works properly on python 3. fix [#1100](https://github.com/Flexget/Flexget/issues/1100)


## 2.0.42 (2016-06-11)
[all commits](https://github.com/Flexget/Flexget/compare/d240ee56641d6aab62d81aad82558c2224473882...275a162ef94e227f7dac70425b73a0113b0a3219)
### Fixed
- return response from get wrapper


## 2.0.41 (2016-06-07)
[all commits](https://github.com/Flexget/Flexget/compare/3452e801f35e61c2530ad8c3fbf69f3bb1e84c31...d240ee56641d6aab62d81aad82558c2224473882)

## 2.0.40 (2016-06-02)
[all commits](https://github.com/Flexget/Flexget/compare/001deaac46bf44198ce27f160e91f664e3e0df64...3452e801f35e61c2530ad8c3fbf69f3bb1e84c31)
### Fixed
- Revert " qualities - Add regex to correctly match webrip quality. Fixes [#1218](https://github.com/Flexget/Flexget/issues/1218)"
- qualities - Add regex to correctly match webrip quality. Fixes [#1218](https://github.com/Flexget/Flexget/issues/1218)


## 2.0.39 (2016-06-01)
[all commits](https://github.com/Flexget/Flexget/compare/6a77ca315dae0c40d384aca5ec7d47ed45a7d97a...001deaac46bf44198ce27f160e91f664e3e0df64)
### Fixed
- imdb list -Forgot sending cookies with list fetch requests
- newnzab - Fixed forcing tvrage ID to be mandatory. Fixes [#1217](https://github.com/Flexget/Flexget/issues/1217)
- API - Change all endpoints to include a trailing slash. Fixes [#1215](https://github.com/Flexget/Flexget/issues/1215)


## 2.0.38 (2016-05-31)
[all commits](https://github.com/Flexget/Flexget/compare/83146096b038ac9fecc5e0d5d9ec1fda2f1e29d7...6a77ca315dae0c40d384aca5ec7d47ed45a7d97a)

## 2.0.37 (2016-05-30)
[all commits](https://github.com/Flexget/Flexget/compare/526de34606ba0f002bd3a0ac3e592f0d04fb7740...83146096b038ac9fecc5e0d5d9ec1fda2f1e29d7)
### Fixed
- - sceper - Wrong string format. Fixes [#1210](https://github.com/Flexget/Flexget/issues/1210)
- flask - Updated calling flask.ext to new method due to flask upgrade to 0.11 to get rid of deprecation warning.
- - imdb_list - Enabled imdb_list to cache credentials per login name ([#1209](https://github.com/Flexget/Flexget/issues/1209)). Fixes [#1109](https://github.com/Flexget/Flexget/issues/1109)


## 2.0.36 (2016-05-30)
[all commits](https://github.com/Flexget/Flexget/compare/062b5a36b9ecdf47eca17e90972430833d7b4020...526de34606ba0f002bd3a0ac3e592f0d04fb7740)
### Fixed
- iptorrents - Fix invalid search string generation, update base_url to use HTTPS


## 2.0.35 (2016-05-28)
[all commits](https://github.com/Flexget/Flexget/compare/4f3e816515d3fe8e21760234f9059013ef077e99...062b5a36b9ecdf47eca17e90972430833d7b4020)

## 2.0.34 (2016-05-26)
[all commits](https://github.com/Flexget/Flexget/compare/9834ccdf821544d23045f57ce6cc717b0a083c94...4f3e816515d3fe8e21760234f9059013ef077e99)

## 2.0.33 (2016-05-25)
[all commits](https://github.com/Flexget/Flexget/compare/62fecfcb83db0f83d430c6c2e80906d232fac3ae...9834ccdf821544d23045f57ce6cc717b0a083c94)
### Fixed
- - movie_list - Added ability to strip_year. Closes [#1128](https://github.com/Flexget/Flexget/issues/1128)


## 2.0.32 (2016-05-25)
[all commits](https://github.com/Flexget/Flexget/compare/c70354070ff5754675f0b1f46b9048310b2f6e77...62fecfcb83db0f83d430c6c2e80906d232fac3ae)
### Fixed
- thetvdb_lookup - api_tvdb did not support date type series lookups. Fixed [#1036](https://github.com/Flexget/Flexget/issues/1036)


## 2.0.31 (2016-05-24)
[all commits](https://github.com/Flexget/Flexget/compare/08e651b880ac7ce3a0b81775c3035ed18bcf39cb...c70354070ff5754675f0b1f46b9048310b2f6e77)

## 2.0.30 (2016-05-22)
[all commits](https://github.com/Flexget/Flexget/compare/2829c33cc6f224595a927f9f665c0ecccb49de27...08e651b880ac7ce3a0b81775c3035ed18bcf39cb)

## 2.0.29 (2016-05-22)
[all commits](https://github.com/Flexget/Flexget/compare/707074dde18cacfb16bec0a3876ce0c38785ca60...2829c33cc6f224595a927f9f665c0ecccb49de27)

## 2.0.28 (2016-05-20)
[all commits](https://github.com/Flexget/Flexget/compare/9beccc2fc78e66e82c298c4ef3fc92890554e689...707074dde18cacfb16bec0a3876ce0c38785ca60)

## 2.0.27 (2016-05-19)
[all commits](https://github.com/Flexget/Flexget/compare/e3220ba202bb9c08ebe3c9e5466d955c6cfef93b...9beccc2fc78e66e82c298c4ef3fc92890554e689)
### Removed
- send_telegram - Removed telegram CLI operations as they were accessing config directly

### Fixed
- - exec - Now function was needlessly added to global jinja2 env. Fixes [#878](https://github.com/Flexget/Flexget/issues/878)


## 2.0.26 (2016-05-18)
[all commits](https://github.com/Flexget/Flexget/compare/a3f1642d5e55df7befd60561c818a27013cd0c5c...e3220ba202bb9c08ebe3c9e5466d955c6cfef93b)
### Fixed
- Fix bad search results from t411 plugin. fix [#1178](https://github.com/Flexget/Flexget/issues/1178)
- execute API - Correctly pass `now` option. Closes [#1132](https://github.com/Flexget/Flexget/issues/1132)


## 2.0.25 (2016-05-17)
[all commits](https://github.com/Flexget/Flexget/compare/911b48dbfe710df447493e7392d819bba023fb98...a3f1642d5e55df7befd60561c818a27013cd0c5c)
### Fixed
- trakt api - Translations lookup was too broad
- trakt lookup - Translations lookup was incorrect, added test
- ftp_list -Fixed param name
- ftp_list - Added logic to avoid unnecessary recursion

### Added
- - trakt lookup API - Added ability to return translations

### Changed
- trakt lookup API - Changed movies endpoint url


## 2.0.24 (2016-05-17)
[all commits](https://github.com/Flexget/Flexget/compare/542e9f9d983c7803545da9f2e8ce8110452f9c5c...911b48dbfe710df447493e7392d819bba023fb98)
### Fixed
- save search results in lowercase, fixes [#1186](https://github.com/Flexget/Flexget/issues/1186)
- simple_persistence upgrade, fixes [#1133](https://github.com/Flexget/Flexget/issues/1133)
- - cron_env - Lower case string comparison. Fixes [#1185](https://github.com/Flexget/Flexget/issues/1185)
- ftp_list - No longer iterating over all dirs, added options for recursion and recursion depth. Closed [#1162](https://github.com/Flexget/Flexget/issues/1162)
- Only send savepath and label to QBittorrent if available, fixes [#1166](https://github.com/Flexget/Flexget/issues/1166)

### Changed
- movie_list CLI - Added movie lookup and set default movie list name to `movies`
- movie_list CLI - Made `list_name` and `movie_title` positional params
- ftp_list - Changed `use_ssl` to just `ssl`
- ftp_list - Removed `regexp` option as filtering should be done on filter phase


## 2.0.23 (2016-05-15)
[all commits](https://github.com/Flexget/Flexget/compare/124ffa67dcee4848086351f33ed26e745ecabf48...542e9f9d983c7803545da9f2e8ce8110452f9c5c)

## 2.0.22 (2016-05-15)
[all commits](https://github.com/Flexget/Flexget/compare/912cfbde0a2fe25804d4a5c2d11be1f22bfb411b...124ffa67dcee4848086351f33ed26e745ecabf48)

## 2.0.21 (2016-05-13)
[all commits](https://github.com/Flexget/Flexget/compare/108fe75531c42e75623e033aa00c2150b04f0a6b...912cfbde0a2fe25804d4a5c2d11be1f22bfb411b)

## 2.0.20 (2016-05-12)
[all commits](https://github.com/Flexget/Flexget/compare/d2c089b7763a8d99afb58822f6d7063c674322b4...108fe75531c42e75623e033aa00c2150b04f0a6b)

## 2.0.19 (2016-05-11)
[all commits](https://github.com/Flexget/Flexget/compare/ac79ec11a0f2dbf9968a21c23f00605d8beb1721...d2c089b7763a8d99afb58822f6d7063c674322b4)
### Fixed
- quality plugin now recognizes 'unknown' quality as a quality.


## 2.0.18 (2016-05-11)
[all commits](https://github.com/Flexget/Flexget/compare/0b195dd77be7feeb2dce071d9787beff1c334c63...ac79ec11a0f2dbf9968a21c23f00605d8beb1721)
### Fixed
- fix crash in torrent_alive fix [#1117](https://github.com/Flexget/Flexget/issues/1117)


## 2.0.17 (2016-05-10)
[all commits](https://github.com/Flexget/Flexget/compare/066dd7fedba43031f3fbce61b534e0cc472149ab...0b195dd77be7feeb2dce071d9787beff1c334c63)
### Changed
- trakt API - Made actors attribute optional


## 2.0.16 (2016-05-09)
[all commits](https://github.com/Flexget/Flexget/compare/99a779e57e00247c3d21ddf737956ae419fd7dc8...066dd7fedba43031f3fbce61b534e0cc472149ab)
### Fixed
- tvmaze_api - Check if series has image attribute. Closes [#1153](https://github.com/Flexget/Flexget/issues/1153)


## 2.0.15 (2016-05-09)
[all commits](https://github.com/Flexget/Flexget/compare/2685c733fdca05032621d8ed49efae2967ae0608...99a779e57e00247c3d21ddf737956ae419fd7dc8)
### Fixed
- only try to use device authorization when called from cli


## 2.0.14 (2016-05-06)
[all commits](https://github.com/Flexget/Flexget/compare/8cb1d9a725eb1d1bdddd499a6061609d1d7e737e...2685c733fdca05032621d8ed49efae2967ae0608)

## 2.0.13 (2016-05-06)
[all commits](https://github.com/Flexget/Flexget/compare/28e712db5aaa8361288ff18557a51c8080df4eb7...8cb1d9a725eb1d1bdddd499a6061609d1d7e737e)

## 2.0.12 (2016-05-05)
[all commits](https://github.com/Flexget/Flexget/compare/6c9901d26b8f59c3535e150f92e4497cabfa56b0...28e712db5aaa8361288ff18557a51c8080df4eb7)
### Fixed
- trakt_lookup API - Fixed API doc for trakt
- trakt_lookup API - Fixed correct date and time object conversions
- movie list - Check for missing movie name before trying to find entry


## 2.0.11 (2016-05-04)
[all commits](https://github.com/Flexget/Flexget/compare/0efcabd42caef081194bc2fe448fb283462806b9...6c9901d26b8f59c3535e150f92e4497cabfa56b0)
### Fixed
- - execute/inject API - Actually pass the options for execution now. Fixed [#1125](https://github.com/Flexget/Flexget/issues/1125), Fixed [#1132](https://github.com/Flexget/Flexget/issues/1132)
- tvmaze API - Remove usage of actors property
- movie list - Fix crash due to incorrect movie name setting and fixed matching via entry IDs

### Changed
- [subliminal] Add option to save to another directory


## 2.0.10 (2016-05-04)
[all commits](https://github.com/Flexget/Flexget/compare/f4de533b15627d2d8a84e6ff2f227ef6889c0115...0efcabd42caef081194bc2fe448fb283462806b9)
### Fixed
- movie_list - titles are now compared in lower case


## 2.0.9 (2016-05-02)
[all commits](https://github.com/Flexget/Flexget/compare/6c356e12758c2121a4f4fb5d9eaeb44fdb9cebbc...f4de533b15627d2d8a84e6ff2f227ef6889c0115)
### Fixed
- Movie List CLI - Added identifier  type validation. Closed [#1116](https://github.com/Flexget/Flexget/issues/1116)
- use native_str_to_text to ensure text fixs [#1097](https://github.com/Flexget/Flexget/issues/1097)


## 2.0.8 (2016-04-29)
[all commits](https://github.com/Flexget/Flexget/compare/94d7e76bbb50e1611e542969f3ed8f0fcbdc6d6d...6c356e12758c2121a4f4fb5d9eaeb44fdb9cebbc)

## 2.0.7 (2016-04-28)
[all commits](https://github.com/Flexget/Flexget/compare/02152ed46ed9dacd6359851e3db54c3b1693403f...94d7e76bbb50e1611e542969f3ed8f0fcbdc6d6d)

## 2.0.6 (2016-04-27)
[all commits](https://github.com/Flexget/Flexget/compare/a06b3d38873db2555143aadeb8931f36586c83af...02152ed46ed9dacd6359851e3db54c3b1693403f)
### Fixed
- Fix crash with sabnzbd plugin on 2.0+ Fix [#1099](https://github.com/Flexget/Flexget/issues/1099)
- Error reporting and fix. Fix [#1099](https://github.com/Flexget/Flexget/issues/1099)


## 2.0.5 (2016-04-26)
[all commits](https://github.com/Flexget/Flexget/compare/f4dba25f09c351f5411b9e28bafac432a1a43fa1...a06b3d38873db2555143aadeb8931f36586c83af)
