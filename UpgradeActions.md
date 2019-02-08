# Required Upgrading Actions
Just planning upgrading? See the [upgrade guide](/Upgrade) first!

## Instructions
This page contains information about configuration file format changes, as well as FlexGet behavioral changes that may affect the user. If your configuration file does not pass `flexget check` after upgrading, this page should contain instructions detailing what you need to change.

Starting from version 2.0.0 we are using semantic versioning, in the form that any increase in the second digit means that configuration is not necessarily backwards compatible and may need to be updated. Therefore this page is generally only updated after each 2.x.0 release.

### **2.20.0** -- Unreleased
#### clean_transmission
The `clean_transmission` plugin has been deprecated. The transmission plugin has gained the ability to remove torrents, which should be used in place of `clean_transmission`. A recipe detailing how to do this can be found [here](/Cookbook/TorrentCleanup). (The deluge plugin has gained the same ability now too.)

`clean_transmission` is still available to use at the moment, but some of its internals had to be tweaked. If you do not immediately replace this plugin, make sure to do a `--test` run to ensure it still causes the behavior you expect.

#### [from_transmission](/Plugins/from_transmission)
The `onlycomplete` option default has been changed from `yes` to `no` in addition to being renamed `only_complete`. By default all entries loaded in transmission will be provided now.

`from_transmission` also provides more entry fields prefixed with `transmission_` with information provided by transmission.

#### [transmission](/Plugins/transmission)
All multi-word options have been changed to have an underscore for consistency and readability. In addition, the spelling of 'honour' has been changed to match the spelling in transmission.
|old name|new name|
|---|---|
|maxupspeed|max_up_speed|
|maxdownspeed|max_down_speed|
|maxconnections|max_connections|
|addpaused|add_paused|
|bandwidthpriority|bandwidth_priority|
|hono**u**rlimits|honor_limits<br/>* *note the spelling change*|

#### [from_deluge](/Plugins/from_deluge)
The `keys` option has been removed. from_deluge now provides all fields from deluge with the `deluge_` prefix. Field names may vary slightly between deluge versions. Do a test run of your task to verify field names after the update:
```sh
flexget --test execute --tasks my_from_deluge_task --dump
```
This will show all available field names and values which you can use to update your config appropriately.

#### [deluge](/Plugins/deluge)
All multi-word options have been changed to have an underscore for consistency and readability.
|old name|new name|
|---|---|
|movedone|move_completed_path|
|queuetotop|queue_to_top|
|automanaged|auto_managed|
|maxupspeed|max_up_speed|
|maxdownspeed|max_down_speed|
|maxconnections|max_connections|
|maxupslots|max_up_slots|
|removeatratio|remove_at_ratio|
|addpaused|add_paused|

### **2.19.0** -- 2019.01.29

Internal sorting of entries has been removed from both the [discover](/Plugins/discover) and [series](/Plugins/series) plugins.

#### Series
Formerly, the series plugin sorted by quality, and when multiple copies of an episode were available on a given run of a task, the highest quality would be chosen. Now that this internal sorting has been removed, the [sort_by](/Plugins/sort_by) plugin can be used in the task to prioritize based on quality, or other metrics. To emulate the old behavior the following can be added to the task:
```yaml
sort_by:
  field: quality
  reverse: yes
```

#### Discover
The discover plugin used to sort all results based upon torrent availability (for search plugins on torrent sites) before adding them to the task. Entries are now released in whatever order the search plugin returns. Torrent search plugins now populate the `torrent_availability` field which can be used if you wish emulate the old behavior.
```yaml
sort_by:
  field: torrent_availability
  reverse: yes
```

### **2.18.0** -- 2019.01.05

If you are using Python 3.7, and you have escape sequences in your regex replacements in `manipulate` plugin, they will need to be double escaped now.

### **2.17.0** -- 2018.10.17

The `deluge` plugin has been changed to use the [deluge-client](https://pypi.org/project/deluge-client/) library. You will need to `pip install deluge-client` if you are using this plugin.

### **2.16.0** -- 2018.10.12

The `variables` plugin has been changed to allow arbitrary sections of config to be substituted. This means it can be used in config sections which require numbers, or even bigger config sections such as a list or dictionary. If you were relying on variable replacement always producing a string, and get config errors after the upgrade, you may need to add extra quotes to the replacement with this version. e.g. `some_setting: "'{? a_variable ?}'"`

The `form` plugin has been changed to use mechanicalsoup rather than mechanize. If you are using this plugin, you'll have to `pip install mechanicalsoup`. It is now python 3 compatible and respects the `headers` plugin.

### **2.14.0** -- 2018.06.24
- Configuration structure for the `irc_daemon` plugins `task_re` option has been modified to treat tasks with more than one pattern defined as an AND condition rather than OR.  This requires modification of existing configurations to the new structure.  More information with an example is available in the updated [`irc_daemon` plugin documentation](https://flexget.com/Plugins/Daemon/irc).
- [`fuzer` search plugin](https://flexget.com/Searches/fuzer) was changed to accomodate site's usage of recaptcha.

### **2.13.0** -- 2018.03.01
Parsing has been greatly simplified. The old interface was difficult to maintain. This also means that the Guessit parser now supports ver. 2.1.4+. Due to the simplification, a lot of the specialized fields such as `is_3d` are no longer available. If you feel that a particular value is missing, open an issue on our [Github](https://www.github.com/Flexget/Flexget/issues).

If you do not make use of Guessit-specific fields, **no** changes to your config are required.

**NOTE**: There are currently a few bugs in Guessit that we have no control over. So if you're parsing anime, it may be better to use the internal parser for now. See [issue #533](https://github.com/guessit-io/guessit/issues/533) and [issue #532](https://github.com/guessit-io/guessit/issues/532).

### **2.12.0** -- 2018.01.26
#### Removed plugins
The following is a list of search plugins that have been removed due to site closures. Any site claiming to be a direct successor/re-opening cannot be trusted.

- Extratorrent
- Freshon
- Sceneaccess
- T411
- Torrent411
- Torrentshack
#### Subliminal
The [subliminal](/Plugins/subliminal) plugin has been changed to reject entries for which it cannot find all requested subtitle languages. Before this change, it would fail entries, but it was deemed counterintuitive.

In addition, single mode will now ignore existing subtitles if the languages do not match. This is the same behaviour as running subliminal manually via CLI.

### **2.10.0** -- 2017.02.17
- Web-UI/API:
  - Changed default UI path to be `hostname:port/` instead of `hostname:port/ui`
  -  Added ability to set `base_url` for web server

### **2.9.0** -- 2017.01.10
#### Notifications:
* [Notification system](/Plugins/Notifiers) has been changed once more. Hopefully we worked most of the kinks out of the new system with this one.
- Backwards compatibility with old system has been taken out; it wasn't working quite properly anyway. You cannot use the [individual notifiers](/Plugins/Notifiers#notifiers) at task level anymore. You must use the [notify](/Plugins/notify) plugin, which is also where message content is now configured. 
- `notify_task`, `notify_entries`, `notify_abort`:
  - plugins removed and combined back into [`notify`](/Plugins/notify) plugin, with subkeys `task`, `entries`, and `abort` subkeys
- `to` option:
  - previously when specifying how a notification should be sent it went under the `to` key. This has been renamed to `via`.
- `file_template`:
  - option has been renamed to `template`
- `notify_osd`:
  - notifier renamed to [`toast`](/Plugins/Notifiers/toast) (and preliminary Windows support added)

- If you use any of the following plugins, you will most likely have to update your config. See their individual wiki pages for the new config format, as well as the [`notify`](/Plugins/notify) plugin.

  - [`email`](/Plugins/Notifiers/email)
  - [`join`](/Plugins/Notifiers/join)
  - [`toast`](/Plugins/Notifiers/toast) (previously `notify_osd`)
  - [`notifymyandroid`](/Plugins/Notifiers/notifymyandroid)
  - [`prowl`](/Plugins/Notifiers/prowl)
  - [`pushalot`](/Plugins/Notifiers/pushalot)
  - [`pushbullet`](/Plugins/Notifiers/pushbullet)
  - [`pushover`](/Plugins/Notifiers/pushover)
  - [`rapidpush`](/Plugins/Notifiers/rapidpush)
  - [`slack`](/Plugins/Notifiers/slack)
  - [`sms_ru`](/Plugins/Notifiers/sms_ru)
  - [`telegram`](/Plugins/Notifiers/telegram)
  - [`xmpp`](/Plugins/Notifiers/xmpp)

- Examples of new notifier config:

  ```yaml
  # Similar to old email config, one message per task run (when there are results)
  notify:
    task:
      template: html  # Optional, if you want html instead of plain text
      via:
        - email:
            to: blah@blah
            # other email opts here
          
  # For push messaging services, one message per accepted entry
  notify:
    entries:
      title: "custom jinja {{title}}"  # Optional
      message: "custom jinja message {{series_name}}"  # Optional
      via:
        - pushbullet:
            opts: here
  ```

#### `secrets`:
- renamed to [`variables`](Plugins/variables) to reflect the more general usage pattern it has gotten.
- The formatting for replacing variables has also been changed so as to not conflict with other jinja in the config file. Example change needed:
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

#### [`if`](/Plugins/if):
- changed to use [jinja expressions](http://jinja.pocoo.org/docs/2.9/templates/#expressions) rather than raw python ones. As the syntax is very similar, most if statements should continue to work correctly.
- If notable changes end up being needed, feel free to come discuss in [chat](Chat) and/or update this space with instructions for others.

### **2.8.0** -- 2016.12.07
- Support for string replacement has been removed. [Jinja2](/Jinja) is the only supported method now.

**The below information is kept for reference, but the notification system was changed again in 2.9.0!**
- Notifier changes, following the feedback from 2.7.0:
  - Created [notify_entries](/Plugins/Notifiers/notify_entries) and [notify_task](/Plugins/Notifiers/notify_task) and deprecated `notify` plugin.
  - Changed `notify_crash` to [notify_abort](/Plugins/Notifiers/notify_abort).
  - Tweaked `file_templates`usage slightly.
  - Added [templates](/CLI/templates) CLI action to get a list of available file templates.

### **2.7.0** -- 2016.11.15
**This information is kept for reference, but the notification system was changed again in 2.9.0!**
- Major change to all notification plugins. Consult new [notifiers](/Plugins/Notifiers) page for name changes and schema changes
- [`email`](/Plugins/Notifiers/email):
  - plugin completely changed, removed cross task functionality (replaced by new [notify](/Plugins/Notifiers/notify) functionality)
- `whatcd`:
  - removed plugin

### **2.6.0** -- 2016.11.15
- [`move`](/Plugins/move), [`copy`](/Plugins/copy): 
  - Changed option `filename` to `rename` since it caused issues with [filesystem](/Plugins/filesystem) plugin.
  - jinja2 replacement render issues will not abort task and not fallback to default.
- [Daemon](/Daemon):
  - `flexget daemon reload` has been renamed to `flexget daemon reload-config` to avoid confusion.
  - `flexget daemon enable-autoreload` and `flexget daemon disable-autoreload` have been removed as their use was limited and ill-conceived.


### **2.5.0** -- 2016.10.21
- [Daemon](/Daemon)/[CLI](/CLI):
  - Due to changes in the IPC protocol, you will not be able to connect to a running daemon that is an earlier version than 2.5.0 using CLI commands. Remember to stop your daemon _before_ upgrading to ensure you can elegantly shut it down.

### **2.4.0** -- 2016.10.18
* [`move`](/Plugins/move), [`delete`](/Plugins/delete), [`copy`](/Plugins/copy):
  * `along` has been greatly simplified and includes similarly named files with specified extensions -- regex/glob no longer supported.
* [Daemon](/Daemon)
  * automatically reloads config before task execution if it detects any changes.
* `tmdb_released`
  * field changed to a Date instead of DateTime ([#1260](https://github.com/Flexget/Flexget/issues/1260))
* Web-UI/API:
  * Major API refactor. Enabling Web-UI/API config changed:
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

* [`discover`](/Plugins/discover):
  * `release_estimations` option now defaults to `strict` instead of `loose`, meaning anything with no release date or one that lies in the future will not be included in the search
  * will now keep searching for new items until it fails to find any (maximum 100 runs). Can be set to the old behaviour using [max_reruns](/Plugins/max_reruns) plugin.
* `movie_queue`:
  * removed along with all related plugins. Use [`movie_list`](/Plugins/List/movie_list) instead.
* `imdb_required`:
  * Removed plugin. Switch to [imdb_lookup](/Plugins/imdb_lookup) and [require_field](/Plugins/require_field).
* [CLI](/CLI):
  * Changed practically all CLI plugins to output using a standardized table [dependency](https://github.com/Robpol86/terminaltables) for a more consistent (and pretty expeirence). Some of the content has been altered in the relevant plugins, and `--porcelain` works slightly different now. See relevant plugin Wiki for details.
* [CLI `trakt`](/CLI/trakt):
  * command `flexget trakt show` has been renamed to `flexget trakt list`
* `subtitle_queue`, `torrentz`, `rutracker`, `newzleech`, `publichd`, `bt-chat`, `btjunkie`, `isohunt`, `redskunk`, `stmusic`:
  * Removed plugins


### **2.2.0** -- 2016.07.27 

* [irc](/Plugins/Daemon/irc):
  * plugin uses outside dependency now. Install with `pip install irc_bot`
* `thetvdb_add`, `thetvdb_remove`, `thetvdb_favorites`:
  * plugins removed. Use [thetvdb_list](/Plugins/List/thetvdb_list) instead.
* `kat`:
  * removed plugin
* `uoccin`:
  * removed all plugins and moved them to [extras](https://github.com/Flexget/extras/) repo.
* [`move`](/Plugins/move), [`copy`](/Plugins/copy), [`delete`](/Plugins/delete)
  * tweaked `along` setting in plugins. See their wiki entries for details.
* [`download`](/Plugins/download), [`move`](/Plugins/move):
  * removed the `output` attribute when using the  plugins. Use `location` instead.

### **2.1.0** -- 2016.06.23
**Several breaking changes**

As an effort to provide more consistent configuration and better user experience, several changes are presented with this version:

* `list_accept`, `list_reject`, `list_queue`:
  * removed plugins. Replaced with [list_match](/Plugins/List/list_match). See plugin page for detailed information on new syntax.
* `emit_series`:
  * changed to [next_series_episodes](/Plugins/next_series_episodes)
* `sonarr_emit`:
  * changed to [next_sonarr_episodes](/Plugins/next_sonarr_episodes)
* `trakt_emit`:
  * changed to [next_trakt_episodes](/Plugins/next_trakt_episodes)
* `send_telegram`:
  * changed to [telegram](/Plugins/telegram)
* `path_select`:
  * changed to [path_by_space](/Plugins/path_by_space)
* `emit_digest`:
  * changed to [from_digest](/Plugins/from_digest)
* `emit_uoccin`:
  * changed to [from_uoccin](/Plugins/from_uoccin)
* `dynamic_imdb`:
  * changed to [from_imdb](/Plugins/from_imdb)
* `trakt_add`, `trakt_remove`:
  * removed and replaced with [`list_add`](/Plugins/List/list_add), [`list_remove`](/Plugins/List/list_remove) and [`trakt_list`](/Plugins/List/trakt_list)

### **2.0.0** -- 2016.04.24
**Major Flexget Change**

Version 2.0.0 of FlexGet introduces Python 3.x support. This was a huge refactor and has been tested to the best of our abilities. With such a huge change like this we expect there to be some bugs, especially with third party plugins. 

For more information on py2/3 code visit [Developers](/https://flexget.com/wiki/Developers).

Please log bugs in [GitHub](/https://github.com/Flexget/Flexget/issues).

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