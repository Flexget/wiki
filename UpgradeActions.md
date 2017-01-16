# Required Upgrading Actions
Just planning upgrading? See [upgrade guide](/Upgrade) first!

## Instructions
This page contains information about configuration file format changes, as well as FlexGet behavioral changes that may affect the user. If your configuration file does not pass `flexget check` after upgrading this page should contain instructions what you need to change.

Starting from version 2.0.0 we are using semantic versioning in the form that any increase in second digit means configuration is not necessarily backwards compatible and needs to be updated.

### **2.9.0** -- 2017.01.10
#### Notifications
[Notification system](/Plugins/Notifiers) has been changed once more. Hopefully we worked most of the kinks out of the new system with this one. Summary of changes:
- Backwards compatibility with old system has been taken out, it wasn't working quite properly anyway. You cannot use the [individual notifiers](/Plugins/Notifiers#notifiers) at task level anymore. You must use the [notify](/Plugins/notify) plugin.
- `notify_task`, `notify_entries`, and `notify_abort` have all been combined back into [notify](/Plugins/notify) plugin, with subkeys `task`, `entries`, and `abort` subkeys.
- Previously when specifying how a notification should be sent it went under the `to` key. This has been renamed to `via`.
- `file_template` option has been renamed to `template`
- The `notify_osd` notifier was renamed to [toast](/Plugins/Notifiers/toast) (and preliminary windows support added)

Examples of new notifier config:

```yaml
# Similar to old email config, one message per task run (when there are results)
notify:
  task:
    template: html  # Optional, if you want html instead of plain text
    via:
      - email:
          to: blah@blah
          # other email opts here
          
```
```yaml
# For push messaging services, one message per accepted entry
notify:
  entries:
    title: "custom jinja {{title}}"  # Optional
    message: "custom jinja message {{series_name}}"  # Optional
    via:
      - pushbullet:
          opts: here
```

#### Secrets plugin
The secrets plugin has been renamed to [variables](Plugins/variables) to reflect the more general usage pattern it has gotten. The formatting for replacing variables has also been changed so as to not conflict with other jinja in the config file. Example change needed:
```yaml
# Before
secrets: mysecrets.yml
tasks:
  a:
    rss: "{{ secrets.myrss }}"
# After
variables: mysecrets.yml
tasks:
  a:
    rss: "{? myrss ?}"
```
If you use notepad++ or another editor capable of doing search and replace with regular expressions, the following may be sufficient (note: only tested in notepad++):
```
find: \{\{\s?secrets\.(.*?)\s?\}\}
replace: \{\? \1 \?\}
```

#### If Plugin
The [if plugin](Plugins/if) has been changed to use [jinja expressions](http://jinja.pocoo.org/docs/2.9/templates/#expressions) rather than raw python ones. As the syntax is very similar, most if statements should continue to work correctly. If notable changes end up being needed, feel free to come discuss in [chat](Chat) and/or update this space with instructions for others.

### **2.8.0** -- 2016.12.07

- Notifier changes, following the feedback from 2.7.0:
  - Created [notify_entries](/Plugins/Notifiers/notify_entries) and [notify_task](/Plugins/Notifiers/notify_task) and deprecated `notify` plugin.
  - Changed `notify_crash` to [notify_abort](/Plugins/Notifiers/notify_abort).
  - Tweaked `file_templates`usage slightly.
  - Added [templates](/CLI/templates) CLI action to get a list of available file templates.
- Support for string replacement has been removed. [Jinja2](/Jinja) is the only supported method now.

### **2.7.0** -- 2016.11.15

- Major change to all notification plugins. Consult new [notifiers](/Plugins/Notifiers) page for name changes and schema changes,
- [email](/Plugins/Notifiers/email) plugin completely changed, removed cross task functionality (replaced by new [notify](/Plugins/Notifiers/notify) functionality)
- Removed `whatcd` plugin

### **2.6.0** -- 2016.11.15
- [move](/Plugins/move)/[copy](/Plugins/copy) plugins: 
  - Changed option `filename` to `rename` since it caused issues with [filesystem](/Plugins/filesystem) plugin.
  - jinja2 replacement render issues will not abort task and not fallback to default.
- Daemon:
  - `flexget daemon reload` has been renamed to `flexget daemon reload-config` to avoid confusion.
  - `flexget daemon enable-autoreload` and `flexget daemon disable-autoreload` have been removed as their use was limited and ill-conceived.


### **2.5.0** -- 2016.10.21
Due to changes in the IPC protocol, you will not be able to connect to a running daemon using cli commands that is an earlier version than 2.5.0. Remember to stop your daemon _before_ upgrading to ensure you can elegantly shut it down.

### **2.4.0** -- 2016.10.18
* Minor changes

  * `along` in `move`, `delete` and `copy` has been greatly simplified and includes similarly named files with specified extensions -- regex/glob no longer supported.
  * daemon automatically reloads config before task execution if it detects any changes.
  * tmdb_released has been changed to a Date instead of DateTime, [#1260](https://github.com/Flexget/Flexget/issues/1260)
* Major API refactor. Enabling WebUi/API config changed:
  ```YAML
  web_server:
    bind: 0.0.0.0 # IP V4
    port: 3539 # Valid port number
    ssl_certificate: '/etc/ssl/private/myCert.pem' # Path to certificate file
    ssl_private_key: '/etc/ssl/private/myKey.key' # Path to private key file
    web_ui: yes # Web-UI can optionally be disabeled, only API will run
  ```
  Or:  
  ```yaml
  web_server: yes
  ```
  That will enable the API and Web-UI on 0.0.0.0 with the port 5050 by default. 
  You can also set a different port using:
  ```yaml
  web_server: 8080
  ```
  API is now always enabled when running the web server, UI is optional (enabled by default).  
  See [Web-UI](/https://flexget.com/Web-UI) and [API](https://flexget.com/API) pages for more detail.

### **2.3.0** -- 2016.08.17 

* [Discover](/Plugins/discover) plugin's `release_estimations` option now defaults to `strict` instead of `loose`, meaning anything with no release date or one that lies in the future will not be included in the search.
* [Discover](/Plugins/discover) will now keep searching for new items until it fails to find any (maximum 100 runs). Can be set to the old behaviour using [max_reruns](/Plugins/max_reruns) plugin.
* Removed deprecated `movie_queue` and all related plugins. Use [movie_list](/Plugins/List/movie_list) instead.
* Removed `imdb_required` plugin, switch to [imdb_lookup](/Plugins/imdb_lookup) and [require_field](/Plugins/require_field)
* Changed practically all CLI plugins to output using a standartized table [dependency](https://github.com/Robpol86/terminaltables) for a more consistent (and pretty expeirence). Some of the content has been altered in the relevant plugins, and `--porcelain` works slightly different now. See relevant plugin Wiki for details.
* CLI command `flexget trakt show` has been renamed to `flexget trakt list`
* Removed `subtitle_queue`plugin
* Removed `rutracker`  plugin
* Removed `torrentz` plugin
* Removed `newzleech` plugin
* Removed `publichd` plugin
* Removed `bt-chat` plugin
* Removed `btjunkie` plugin
* Removed `isohunt` plugin
* Removed `redskunk` plugin
* Removed `stmusic` plugin


### **2.2.0** -- 2016.07.27 

* [irc](/Plugins/Daemon/irc) plugin uses outside dependency now. Install with `pip install irc_bot`
* Removed `thetvdb_add`, `thetvdb_remove` and `thetvdb_favorites`. Use [thetvdb_list](/Plugins/List/thetvdb_list) instead.
* Removed `kat` search plugin. 
* Removed all `uoccin` plugins. Moved them to [extras](https://github.com/Flexget/extras/) repo.
* Tweaked `along` setting in [move](/Plugins/move), [copy](/Plugins/copy) and [delete](/Plugins/delete) plugins. See their wiki for details.
* Removed the `output` attribute when using the [download](/Plugins/download) and [move](/Plugins/move) plugins. Use `location` instead.

### **2.1.0** -- 2016.06.23
**Several breaking changes**

As an effort to provide more consistent configuration and better user experience, several changes are presented with this version:

* `list_accept`, `list_reject` and `list_queue` plugins have been replaced with [list_match](/Plugins/List/list_match). See plugin page for detailed information on new syntax.
* Changed `emit_series` to [next_series_episodes](/Plugins/next_series_episodes)
* Changed `sonarr_emit` to [next_sonarr_episodes](/Plugins/next_sonarr_episodes)
* Changed `trakt_emit` to [next_trakt_episodes](/Plugins/next_trakt_episodes)
* Changed `send_telegram` to [telegram](/Plugins/telegram)
* Changed `path_select` to [path_by_space](/Plugins/path_by_space)
* Changed `emit_digest` to [from_digest](/Plugins/from_digest)
* Changed `emit_uoccin` to [from_uoccin](/Plugins/from_uoccin)
* Changed `dynamic_imdb` to [from_imdb](/Plugins/from_imdb)
* Removed the deprecated `trakt_add` and `trakt_remove`

### **2.0.0** -- 2016.04.24
**Major Flexget Change**

Version 2.0.0 of FlexGet introduces python3.x support. This was a huge refactor and has been tested to be best of our abilities. With such a huge change like this we expect there to be some bugs especially with third party plugins. 

For more information on py2/3 code visit [https://flexget.com/wiki/Developers](/https://flexget.com/wiki/Developers)

Please log bugs to [https://github.com/Flexget/Flexget/issues](/https://github.com/Flexget/Flexget/issues)

### 1.2.505 -- 2016.04.07
**Series CLI Changes:**

* Series CLI - `series forget` now also fires a `forget` event which for now removes all the relevant downloaded release from `seen` plugin as well. This is relevant both for entire series and when using identifer.
* Series CLI - `series remove` was added which does what `series forget` used to do, I.E. remove show/episode only from series DB
* Series API - `remove_seen` parameter name was changed to `forget` in all the DELETE endpoints.
* Changed `series_forget` plugin name to `series_remove`

**List interface:**

A new convention of plugins that allows usage as input, filter and output. See [wiki page](https://flexget.com/wiki/Plugins/List) for additional information.
* [imdb_list](https://flexget.com/wiki/Plugins/List/imdb_list) plugin has changed attributes (and can now be used to add, remove or filter movies from IMDB watchlist directly).
* `couchpotato` changed its name to `couchpotato_list`.
* `sonarr` changed its name to `sonarr_list`.

### 1.2.502 -- 2016.04.04 
TVDB API has changed, now requires account_id (userkey) rather then user password.

TVDB plugins 'password' field has been changed to 'account_id'. To get your account_id visit http://thetvdb.com/?tab=userinfo

### 1.2.496 -- 2016.03.28
Plugin rlslog has been removed and is no longer supported

### 1.2.484 -- 2016.03.16
All TVDB plugins have been upgraded to use the new TVDB API [api-beta.thetvdb.com/swagger#/](/api-beta.thetvdb.com/swagger#/)

Due to the change in API the `account_id` can no longer be used within tvdb plugins, it now requires `username` and `password` within your config.

The fields `tvdb_ep_writers` and `tvdb_ep_guest_stars` are no longer supported.

Field `tvdb_banner_url` changed to `tvdb_banner`
Field `tvdb_poster_url` changed to `tvdb_posters` which is a list of the top 5 posters.


### 1.2.471 -- 2016.03.05
Python 2.6 is no longer being supported by FlexGet. Support for python 2.6 itself ended October 2013, and it is no longer receiving even security updates. You should upgrade to python 2.7 if you have not done so already.

### 1.2.464 -- 2016.02.29
The `ignore_estimations` option in the [Discover](https://flexget.com/wiki/Plugins/discover) plugin was changed and now it should be used as `release_estimations`. See plugin page for further information. If you did not use that option, no action is needed.

### 1.2.455 -- 2016.02.18
The `urlrewrite_redirect` plugin, which previously rewrite all accepted entries' urls to any url they redirected to has been disabled by default. If you need this behavior, you must add `redirect_url: yes` to your task.

### 1.2.452 -- 2016.02.11
The `listdir` and `find` plugins (which have been deprecated for a while) have now been removed. Their functionality can be replicated with the [filesystem](/Plugins/filesystem) plugin. If you haven't already, you will need to make this change in your config.

Deluge 1.1 support has been removed from the deluge plugin.

### 1.2.446 -- 2016.02.02
The markdown option in the [Telegram plugin](https://flexget.com/wiki/Plugins/send_telegram) was changed from `use_markdown` to `parse_mode` and it now accept either `markdown` or `html`. Update your configurations accordingly. [Telegram API page for more details](https://core.telegram.org/bots/api#formatting-options). Also, the minimal required version of `python-telegram-bot` is `3.2.0`. Upgrade using `pip install python-telegram-bot --upgrade`.

### ?? -- 2015.12.29

**t411 replace torrent411 for discovering**

The search plugin is called henceforth `t411` instead of `torrent411`. Credentials are no longer setted into config file ; remove `username` and `password` and setting up definetively your credentials via CLI `flexget t411 add-auth <username> <password>`. Category and terms names are now the same as on the website. For example, `HDrip-720p` becomes `HDrip 720`.

**t411 replace torrent411 urlrewritter for as input plugin**

You can no longer use the plugin `html` or `rss` for scraping the Torrent411 website. Instead, use the [t411 input plugin](/Plugins/t411).

### 1.2.410 -- 2015.12.16 
Due to a complete refactor of [Pushover plugin](https://flexget.com/wiki/Plugins/pushover), the field `urltitle` need to be changed to `url_title` in config. Users that do not use that field in their Pushover plugin config do not need to change anything, and all should work well.

### 1.2.389 --2015.11.15 
TVRage seems to be down, so in its place we have implemented [TVMaze](http://www.tvmaze.com), which requires a few new dependencies.
If you are installed from a git checkout, you'll have to make sure your deps are up to date after pulling. Run `bin/pip install --upgrade -e .` from your checkout directory if you are using the virtualenv setup that bootstrap.py gives you.

### 1.2.385 -- 2015.11.11
**trakt 2.0 api update**

The trakt plugins have been updated to use the newest API (v2). Authorization is now handled by tokens. You can generate a pin for Flexget by visiting https://trakt.tv/pin/346. Use this pin to generate an access token by issuing the cli command `flexget trakt auth <account> <pin>`, where `<account>` is a local identifier that the access token is assigned to. We recommend that you use your Trakt username.

**general changes for all trakt plugins**

They no longer require `password` and so this option should be deleted from your config. Instead it takes a new argument `account`. Specifying an `account` is required to access anything private/protected on trakt. You must specify either `account` or `username`. If `account` is specified without `username`, the owner of the account will be the assumed username.

Affected Plugins:
  - [trakt_list](/Plugins/trakt_list)
  - [trakt_emit](/Plugins/trakt_emit)
  - [trakt_add](/Plugins/trakt_add)
  - [trakt_remove](/Plugins/trakt_remove)
  - [trakt_lookup](/Plugins/trakt_lookup)

**trakt_collected_lookup / trakt_watched_lookup**

These plugins have been merged with `trakt_lookup` and no longer exist. You'll need to specify the `account` option in [trakt_lookup](/Plugins/trakt_lookup) in order for the related fields to be looked up.

**trakt_lookup**

Now supports movie lookups as well as episode and show lookups. It also takes two optional arguments `username` and `account`. Specifying a `username` enables the previous functionality of `trakt_collected_lookup` and `trakt_watched_lookup`, which provide two new entry fields `trakt_collected` and `trakt_watched` respectively. These new fields indicate whether the entry has been collected or watched by the trakt user specified in `username` argument. 

`trakt_lookup: yes` will enable the basic trakt lookup in your tasks.

### 1.2.362 -- 2015.10.13 
**find / listdir**

The `find` and `listdir` plugins have been merged into one [filesystem](/Plugins/filesystem) plugin. You will need to replace both in your config with just `filesystem`.

### 1.2.359 -- 2015.10.09
A json api has been added which requires a few new dependencies. If you are installed from a git checkout, you'll have to make sure your deps are up to date after pulling. `bin/pip install --upgrade -e .` from your checkout directory if you are using the virtualenv setup that bootstrap.py gives you.

### 1.2.261 -- 2015.01.12
`disable_builtins` and `disable_plugin` plugins have been combined into the [disable](/Plugins/disable) plugin. You will need to replace both in your config with just `disable`. If you were using `disable_builtins: yes` form, this should be changed to `disable: builtins`

### 1.2.247 -- 2015.01.01
**movie_queue / queue_movies**

The `movie_queue` plugin has been enhanced to include the ability to add & remove movies removing the need for the `queue_movies` plugin. You will need to replace `movie_queue: yes` with `movie_queue: accept` to add any accepted items in the movie queue. Also, `queue_movies: yes` is replaced by `movie_queue: add`, which adds items to the movie queue.

**trakt_emit / trakt_add / trakt_remove**

These plugins have been update to use trakt api v2. They no longer need `api_key`, which should be deleted from their config options. The built-in list names have been standardized to `watchlist`, `watched`, and `collection`.

**trakt_list**

Trakt list has been updated to api v2, and the config has been made more consistent with the other trakt plugins. The built-in list names have been standardized to `watchlist`, `watched`, and `collection`. Listing episodes from custom lists is now also possible. `api_key` option should be removed from config. The list and type should now be specified as two separate options, e.g.
```
trakt_list:
  username: me
  api_key: blah
  movies: watchlist
```
would now become:
```
trakt_list:
  username: me
  list: watchlist
  type: movies
```