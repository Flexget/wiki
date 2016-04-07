= Required Upgrading Actions =

Just planning upgrading? See [wiki:Upgrade upgrade guide] first!

'''{{{NOTE:}}}''' You can use this [http://feed43.com/flexget_upgrade_actions.xml RSS Feed] to keep up with "major" changes.

== Instructions ==


This page contains information about configuration file format changes, as well as !FlexGet behavioral changes that may affect the user. If your configuration file does not pass {{{flexget check}}} after upgrading this page should contain instructions what you need to change.

=== 2016.4.7 1.2.505 ===

**Series CLI Changes:**

* Series CLI - `series forget` now also fires a `forget` event which for now removes all the relevant downloaded release from `seen` plugin as well. This is relevant both for entire series and when using identifer.
* Series CLI - `series remove` was added which does what `series forget` used to do, I.E. remove show/episode only from series DB
* Series API - `remove_seen` parameter name was changed to `forget` in all the DELETE endpoints.
* Changed `series_forget` plugin name to `series_remove`

**List interface:**

A new convention of plugins that allows usage as input, filter and output. See [http://flexget.com/wiki/Plugins/List wiki page] for additional information.
* [http://flexget.com/wiki/Plugins/List/imdb_list imdb_list] plugin has changed attributes (and can now be used to add, remove or filter movies from IMDB watchlist directly).
* `couchpotato` changed its name to `couchpotato_list`.
* `sonarr` changed its name to `sonarr_list`.

=== 2016.4.4 1.2.502 ===

TVDB API has changed, now requires account_id (userkey) rather then user password.

TVDB plugins 'password' field has been changed to 'account_id'. To get your account_id visit http://thetvdb.com/?tab=userinfo

=== 2016.3.28 1.2.496 ===

Plugin rlslog has been removed and is no longer supported

=== 2016.3.16 1.2.484 ===

All TVDB plugins have been upgraded to use the new TVDB API [api-beta.thetvdb.com/swagger#/]

Due to the change in API the `account_id` can no longer be used within tvdb plugins, it now requires `username` and `password` within your config.

The fields `tvdb_ep_writers` and `tvdb_ep_guest_stars` are no longer supported.

Field `tvdb_banner_url` changed to `tvdb_banner`
Field `tvdb_poster_url` changed to `tvdb_posters` which is a list of the top 5 posters.


=== 2016.3.5 1.2.471 ===

Python 2.6 is no longer being supported by !FlexGet. Support for python 2.6 itself ended October 2013, and it is no longer receiving even security updates. You should upgrade to python 2.7 if you have not done so already.

=== 2016.2.29 1.2.464 ===
The `ignore_estimations` option in the [http://flexget.com/wiki/Plugins/discover Discover] plugin was changed and now it should be used as `release_estimations`. See plugin page for further information. If you did not use that option, no action is needed.

=== 2016.2.18 1.2.455 ===
The `urlrewrite_redirect` plugin, which previously rewrite all accepted entries' urls to any url they redirected to has been disabled by default. If you need this behavior, you must add `redirect_url: yes` to your task.

=== 2016.2.11 1.2.452 ===
The `listdir` and `find` plugins (which have been deprecated for a while) have now been removed. Their functionality can be replicated with the [wiki:Plugins/filesystem filesystem] plugin. If you haven't already, you will need to make this change in your config.

Deluge 1.1 support has been removed from the deluge plugin.

=== 2016.2.2 1.2.446 ===
The markdown option in the [http://flexget.com/wiki/Plugins/send_telegram Telegram plugin] was changed from `use_markdown` to `parse_mode` and it now accept either `markdown` or `html`. Update your configurations accordingly. [https://core.telegram.org/bots/api#formatting-options Telegram API page for more details]. Also, the minimal required version of `python-telegram-bot` is `3.2.0`. Upgrade using `pip install python-telegram-bot --upgrade`.

=== Comming soon ===
'''t411 replace torrent411 for discovering'''

The search plugin is called henceforth {{{t411}}} instead of {{{torrent411}}}. Credentials are no longer setted into config file ; remove {{{username}}} and {{{password}}} and setting up definetively your credentials via CLI {{{flexget t411 add-auth <username> <password>}}}. Category and terms names are now the same as on the website. For example, {{{HDrip-720p}}} becomes {{{HDrip 720}}}.

'''t411 replace torrent411 urlrewritter for as input plugin'''

You can no longer use the plugin {{{html}}} or {{{rss}}} for scraping the Torrent411 website. Instead, use the [wiki:Plugins/t411 t411 input plugin].

=== 2015.12.29 X.X.XXX ===
The markdown option in the [http://flexget.com/wiki/Plugins/send_telegram Telegram plugin] was changed from use-markdown to use_markdown. Update your configurations accordingly.

=== 2015.12.16 1.2.410 ===

Due to a complete refactor of [http://flexget.com/wiki/Plugins/pushover Pushover plugin], the field `urltitle` need to be changed to `url_title` in config. Users that do not use that field in their Pushover plugin config do not need to change anything, and all should work well.

=== 2015.11.15 1.2.389 ===

TVRage seems to be down, so in its place we have implemented [http://www.tvmaze.com TVMaze], which requires a few new dependencies.
If you are installed from a git checkout, you'll have to make sure your deps are up to date after pulling. Run `bin/pip install --upgrade -e .` from your checkout directory if you are using the virtualenv setup that bootstrap.py gives you.

=== 2015.11.11 1.2.385 ===
'''trakt 2.0 api update'''

The trakt plugins have been updated to use the newest API (v2). Authorization is now handled by tokens. You can generate a pin for Flexget by visiting https://trakt.tv/pin/346. Use this pin to generate an access token by issuing the cli command `flexget trakt auth <account> <pin>`, where `<account>` is a local identifier that the access token is assigned to. We recommend that you use your Trakt username.

'''general changes for all trakt plugins'''

They no longer require `password` and so this option should be deleted from your config. Instead it takes a new argument `account`. Specifying an `account` is required to access anything private/protected on trakt. You must specify either `account` or `username`. If `account` is specified without `username`, the owner of the account will be the assumed username.

Affected Plugins:
  - [wiki:Plugins/trakt_list trakt_list]
  - [wiki:Plugins/trakt_emit trakt_emit]
  - [wiki:Plugins/trakt_add trakt_add]
  - [wiki:Plugins/trakt_remove trakt_remove]
  - [wiki:Plugins/trakt_lookup trakt_lookup]

'''trakt_collected_lookup / trakt_watched_lookup'''

These plugins have been merged with `trakt_lookup` and no longer exist. You'll need to specify the `account` option in [wiki:Plugins/trakt_lookup trakt_lookup] in order for the related fields to be looked up.

'''trakt_lookup'''

Now supports movie lookups as well as episode and show lookups. It also takes two optional arguments `username` and `account`. Specifying a `username` enables the previous functionality of `trakt_collected_lookup` and `trakt_watched_lookup`, which provide two new entry fields `trakt_collected` and `trakt_watched` respectively. These new fields indicate whether the entry has been collected or watched by the trakt user specified in `username` argument. 

`trakt_lookup: yes` will enable the basic trakt lookup in your tasks.

=== 2015.10.13 1.2.362 ===
'''find / listdir'''

The `find` and `listdir` plugins have been merged into one [wiki:Plugins/filesystem filesystem] plugin. You will need to replace both in your config with just `filesystem`.

=== 2015.10.09 1.2.359 ===
A json api has been added which requires a few new dependencies. If you are installed from a git checkout, you'll have to make sure your deps are up to date after pulling. `bin/pip install --upgrade -e .` from your checkout directory if you are using the virtualenv setup that bootstrap.py gives you.

=== 2015.1.12 1.2.261 ===
`disable_builtins` and `disable_plugin` plugins have been combined into the [wiki:Plugins/disable disable] plugin. You will need to replace both in your config with just `disable`. If you were using `disable_builtins: yes` form, this should be changed to `disable: builtins`

=== 2015.1.1 1.2.247 ===
'''movie_queue / queue_movies'''

The `movie_queue` plugin has been enhanced to include the ability to add & remove movies removing the need for the `queue_movies` plugin. You will need to replace `movie_queue: yes` with `movie_queue: accept` to add any accepted items in the movie queue. Also, `queue_movies: yes` is replaced by `movie_queue: add`, which adds items to the movie queue.

'''trakt_emit / trakt_add / trakt_remove'''

These plugins have been update to use trakt api v2. They no longer need `api_key`, which should be deleted from their config options. The built-in list names have been standardized to `watchlist`, `watched`, and `collection`.

'''trakt_list'''

Trakt list has been updated to api v2, and the config has been made more consistent with the other trakt plugins. The built-in list names have been standardized to `watchlist`, `watched`, and `collection`. Listing episodes from custom lists is now also possible. `api_key` option should be removed from config. The list and type should now be specified as two separate options, e.g.
{{{
trakt_list:
  username: me
  api_key: blah
  movies: watchlist
}}}
would now become:
{{{
trakt_list:
  username: me
  list: watchlist
  type: movies
}}}