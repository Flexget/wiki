= Required Upgrading Actions =

Just planning upgrading? See [wiki:Upgrade upgrade guide] first!

== Instructions ==

This page contains information about configuration file format changes, as well as !FlexGet behavioral changes that may affect the user. If your configuration file does not pass {{{--check}}} after upgrading this page should contain instructions what you need to change.

=== 2013.2.12 1.0.3348 ===
All entry fields provided by [wiki:Plugins/thetvdb_lookup thetvdb_lookup] have been updated to have a 'tvdb_' prefix. If you are using these fields in your config or custom template, you will need to update them. For the most part fields with a 'series_' prefix have been replaced with 'tvdb_' prefix, and fields with an 'ep_' prefix have had the 'tvdb_' prefix added. 'thetvdb_id' has been renamed to 'tvdb_id' and 'series_name_tvdb' has been renamed to 'tvdb_series_name'. The updated list of fields can be found on the [wiki:Plugins/thetvdb_lookup thetvdb_lookup] page.

=== 2013.2.4 1.0.3334 ===

The {{{all_entries}}} option for [wiki:Plugins/rss rss] plugin has been changed to be on by default. If you would like to improve performance on your task by having the rss plugin only emit entries once, you must manually turn this option on.

=== 2013.2.2 ===

If you get critical error:

{{{
Error while registering plugin metainfo_task. A plugin with the name metainfo_task is already registered
}}}

or

{{{
File "/usr/local/lib/python2.7/dist-packages/flexget/plugins/metainfo/feed.py", line 7, in <module>
    class MetainfoTask(plugin.BuiltinPlugin):
AttributeError: 'module' object has no attribute 'BuiltinPlugin'
}}}

The upgrade has left "feed.py" behind in python's site-packages. Remove !FlexGet directory from site-packages or dist-packages and reinstall !FlexGet.

=== 4.10.2012 r3158 ===
The [wiki:Searches/kat kat] search plugin was updated to use {{{verified}}} option. You will need to update your conifg if you are using it.
{{{
# Old way
kat: <category>
# New way
kat:
  category: <category>
}}}

=== 18.9.2012 r3147 ===
The [wiki:Searches/torrentz torrentz] search plugin now takes a single option, the reputation required of the results. See wiki page for options. You must change your config from:
{{{
torrentz
}}}
to
{{{
torrentz: good
}}}
(or any other valid reputation) upon upgrade.

=== 7.9.2012 r3139 ===
Svn & git users need to install a newer version or requests (0.14+) manually, either rerun {{{bootstrap.py}}} or simply run {{{bin/pip install --upgrade requests}}} on checkout dir.

=== 1.9.2012 r3130 ===
Options have been added to the [wiki:Searches/piratebay piratebay] search plugin. To continue using it the same way you are now, you must change {{{piratebay}}} in your config to {{{piratebay: yes}}}. You can also specify category and sort options instead of the default if you choose.

=== 14.8.2012 r3078 ===
!BeautifulSoup 4 is now needed as well as BS3. If you are on svn or virtualenv install, you will need to install it: {{{bin/pip install beautifulsoup4}}} (easy_install/pip users don't need to do anything special)

=== 3.8.2012 r3061 ===

{{{feeds}}} have now been renamed to {{{tasks}}}. You need to update your config to use the new term. Also, if you have any custom templates that used feed properties, you'll need to update them as well. If you notice any problems related to this refactoring, please submit a bug ticket.

If past problems are any indication, some users may also need to delete feed.py and .pyc from their install directory manually.

=== 10.7.2012 r3021 ===

Svn & git users need to install argparse manually, either rerun {{{bootstrap.py}}} or simply run {{{bin/pip install argparse}}} on checkout dir.

=== 24.6.2012 r2977 ===

The {{{reject_failed}}} plugin has been refactored into the [wiki:Plugins/retry_failed retry_failed] plugin. If you were changing the retry count, or otherwise using the plugin in your config, you will need to update it. Please read the [wiki:Plugins/retry_failed retry_failed] docs for more info.

Sometimes the upgrade does not delete the old files, if you are getting an error like {{{sqlalchemy.exc.InvalidRequestError: Table 'failed' is already defined for this MetaData instance}}} or {{{Two different schema versions recieved for plugin failed}}}. You'll have to manually delete the old files. <installdir>/plugins/filter/reject_failed.py and .pyc need to be deleted.

=== 12.6.2012 r2943 ===
By default the [wiki:Plugins/rss rss] plugin will no longer produce the same entries more than once. If you want all of the entries to be produced every run, you can use the {{{all_entries: yes}}} option. This option also replaces the old {{{etag}}} option, so {{{etag: no}}} will need to be changed to {{{all_entries: yes}}} in your config. If you were using the [wiki:Plugins/only_new only_new] plugin to accomplish this before, you should now remove it from the feed, as the rss plugin's built in handling is much more efficient.

The [wiki:Jinja#Jinja2Filters pathscrub jinja filter] has been refactored to use the [wiki:Plugins/pathscrub pathscrub] plugin. You os setting with the pathscrub plugin will be respected when you use the pathscrub jinja filter, and the parameters to the jinja filter have been changed so that you can override the os.

=== 30.5.2012 r2893 ===
'''{{{ATTENTION:}}}''' This is a major change in how !FlexGet handles qualities. You '''will''' need to update your configuration to make sure everything works properly in the new system. First you should read [wiki:Qualities this page] to find out how the new system works. Then you can use the following information to upgrade your config to the new system:

''' [wiki:Plugins/series Series] Plugin Changes '''

The {{{min_quality}}} and {{{max_qaulity}}} options have been removed. These are replaced by the normal {{{quality}}} option, as it now supports ranges directly. The other major change is to the {{{timeframe}}} feature. Instead of defining your desired quality with the {{{quality}}} option, you define it in the new option {{{target}}}. Your {{{quality}}} setting will continue to be respected, even after the timeframe has expired.

Here is an example config change that would be required.
Old way:
{{{
series:
  settings:
    groupa:
      quality: 720p
      timeframe: 6 hours
      min_quality: hdtv
      max_quality: 720p
    groupb:
      quality: hdtv
}}}
New way:
{{{
series:
  settings:
    groupa:
      target: 720p
      timeframe: 6 hours
      quality: hdtv+ <=720p
    groupb:
      # Since source and resolution are different categories now, you need to define that you don't want 720p and above in order to approximate old 'hdtv' quality.
      quality: hdtv <720p 
}}}

''' [wiki:Plugins/quality Quality] Plugin Changes '''

{{{min}}} and {{{max}}} options have been removed, ranges can be specified without them now.
Config, old way:
{{{
quality:
  min: 720p
  max: 1080p
}}}
New way: (You probably want to add the a source requirement, like dsr+ bit here so that you don't get 'cam' or 'workprint' etc. sources)
{{{
quality: 720p-1080p dsr+
}}}

''' [wiki:Plugins/movie_queue Movie Queue] Plugin (and [wiki:Plugins/queue_movies Queue Movies]) Changes '''

When adding a movie to the queue, either via CLI or through queue_movies plugin, you can now specify quality in the new manner.

Examples:
{{{
flexget --movie-queue add "A Good Movie" "720p+ bluray+"
}}}
{{{
queue_movies:
  quality: 720p-1080p bluray
}}}

=== 28.2.2012 r2757 (d.m.yyyy) ===

The series parser has been upgraded to support two new modes, {{{sequence}}} and {{{date}}}. If you are using {{{identified_by: id}}} in your config to match dated or absolutely numbered series, you will have to change it to the appropriate new mode. In addition, for series that were auto detected as identified_by id, they will need to be re-detected based on the upcoming episodes. You may get a few weird matches until it decides upon the new mode. See [wiki:Plugins/series/identified_by here] for more information.

'''SVN users:''' You will have to run {{{bin/paver clean}}} and {{{python bootstrap.py}}} to make sure all dependencies are installed correctly in your virtualenv.

=== xx.02.2012 r2700 (d.m.yyyy) ===

Certain SQLAlchemy and Request libraries are currently not working with !FlexGet so you may need to downgrade them if you get errors like.

{{{
pkg_resources.DistributionNotFound?: requests>=0.10,!=0.10.1,<0.11 
}}}

You can use pip / easy_install to install specific version.

{{{
pip --upgrade install requests==0.10.0
pip --upgrade install sqlalchemy==0.7.4
}}}

We will try to make application compatible with latest versions soon.

=== 27.12.2011 r2607 (d.m.yyyy) ===

SVN users should make sure feedparser is at least version 5.1 due to a bug exposed in lower versions. see #1405
{{{
bin/easy_install --upgrade feedparser
}}}

=== 27.12.2011 r2601 (d.m.yyyy) ===

The python [http://docs.python-requests.org/en/latest/ requests library] has been added as a dependency. SVN users will need to manually install it to their virtualenv:
{{{
bin/pip install requests
}}}

=== 11.12.2011 r2513 (d.m.yyyy) ===

The search plugin has been renamed to urlrewrite_search.

=== 7.12.2011 r2493 (d.m.yyyy) ===

Feeds and presets are no longer allowed to be named the same as any plugins.

=== 16.10.2011 r2430 (d.m.yyyy) ===

input_deluge plugin has been renamed from_deluge

=== 2x.5.2011 r2xxx (d.m.yyyy) ===

If you're running subversion and get this error #1112 run

{{{
bin/pip install --upgrade sqlalchemy
}}}

=== 22.5.2011 r2238 (d.m.yyyy) ===

[wiki:Plugins/imdb_queue imdb_queue] plugin has been replaced by [wiki:Plugins/movie_queue movie_queue]. Movies in the imdb queue will automatically be transferred to movie queue, your config will need manually updated. From now on --movie-queue should be used instead of --imdb-queue.

=== 1.4.2011 r2125 (d.m.yyyy) ===

Upgrade movie related qualities from config, eg. `720p` to `720p bluray` and `1080p` to `1080p bluray`. Also use these qualities with `--imdb-queue´ from now on.

=== 2.2.2011 (d.m.yyyy) ===

If you have very old installation / database, you might want to run:

{{{
sqlite3 db-config.sqlite "CREATE INDEX ix_imdb_movies_url ON imdb_movies (url);"
}}}

This will improve performance with imdb lookups from the cache.

=== 30.1.2011 r1899 (d.m.yyyy) ===

[wiki:Plugins/thetvdb_favorites thetvdb_favorites] has been refactored into an input plugin for use with [wiki:Plugins/import_series import_series]. To upgrade your config, if it used to be:
{{{
thetvdb_favorites:
  account_id: xxxx
  quality: 720p
}}}
It should now be:
{{{
import_series:
  settings:
    quality: 720p
  from:
    thetvdb_favorites:
      account_id: xxxx
}}}

=== 27.1.2011 r1891 (d.m.yyyy) ===

[wiki:Plugins/rss rss] plugin option {{{group links}}} has been changed to {{{group_links}}} to be consistent with the other options. Update your config if you are using it.

=== 23.1.2011 r1888 (d.m.yyyy) ===

Plugins exec and manipulate configuration was slightly changed due refactoring, if you've used `event` option it needs to be changed to `phase`.

=== 21.1.2011 r1877 (d.m.yyyy) ===

The format_field plugin has been removed. Its functionality has been taken over by the [wiki:Plugins/set set] plugin, so your config must be updated to use that instead.

=== Subversion users: 17.12.2010   ===

If you get message "FATAL: SQLAlchemy 0.6.0 or newer required. Please upgrade your SQLAlchemy." 

Run:

{{{
bin/paver clean
python bootstrap.py
}}}

This will re-bootstrap the environment from clean state and install all new dependencies etc.

=== 24.11.2010 r1661 (d.m.yyyy) ===

metainfo_series is no longer a builtin. This should only affect you if you aren't using one of the series plugins (series, all_series, thetvdb_favorites, or series_premiere.) If you need to enable metainfo_series manually for a feed it can be done like so:

{{{
metainfo_series: yes
}}}

=== 16.11.2010 r1643 (d.m.yyyy) ===

The [wiki:Plugins/series series] plugin {{{all}}} mode has been moved in to it's own plugin, [wiki:Plugins/all_series all_series]. The config format for both [wiki:Plugins/thetvdb_favorites thetvdb_favorites] and [wiki:Plugins/series_premiere series_premiere] has been changed to allow all settings from the [wiki:Plugins/series series] plugin. Specifically, if you were using this format for the series_premiere plugin:

{{{
series_premiere: <path>
}}}

you must update to:

{{{
series_premiere:
  path: <path>
}}}

=== 14.11.2010 r1639 (d.m.yyyy) ===

The transmissionrpc plugin has been renamed to [wiki:Plugins/transmission transmission]. Your config must be updated to reflect this.

=== 10.11.2010 r1620 (d.m.yyyy) ===

[wiki:Plugins/exec Exec] plugin no longer escapes anything by default during string substitution. If your fields might contain something that needs escaped, you can use the [wiki:Plugins/exec?version=9#Autoescapeoption auto_escape] option to have all non word characters escaped with backslash.

=== 9.11.2010 r1617 (d.m.yyyy) ===

The [wiki:Plugins/exec exec] plugin no longer tries to do any automatic quoting on string replaced variables. Instead, the values that get replaced will have any contained quotes escaped with a backslash. This means the command now gets passed as it appears in your config to the shell to be executed. If you are using a variable that may contain spaces, you have to manually add quotes around that argument in your command now. Alternatively, you may have to stop escaping quotes in your command if you were doing so to have them to have them survive the automatic quoting process. (see #800)

=== 3.11.2010 r1582 (d.m.yyyy) ===

There were some changes to how the _excluding operations work when multiple regexps have been defined in the [wiki:Plugins/regexp regexp] plugin.
Before, reject_excluding would reject if an entry omitted ''all'' of the listed regexps, now it will reject if an entry omits ''any'' of the listed regexps. (same goes for accept_excluding)

For example, this config:

{{{
regexp:
  reject_excluding:
    - titleA
    - groupB
}}}

Will now reject an entry called {{{titleA.something}}} but not {{{titleA.groupB}}}

If you were using the old behavior, you can achieve the same thing by altering your regexp to be like this:

{{{
  reject_excluding:
    - titleA|groupB
}}}

Which would not reject either {{{titleA.something}}} or {{{groupB.something}}}

=== 30.10.2010 r1570 (d.m.yyyy) ===

Two new qualities were added, {{{720p web-dl}}} and {{{1080p web-dl}}}. In addition, the plain {{{web-dl}}} quality has been lowered in priority. You might need to update your config to match the new [wiki:Qualities quality hierarchy].

=== 24.10.2010 r1552 (d.m.yyyy) ===

The [wiki:Plugins/exec exec] and [wiki:Plugins/adv_exec adv_exec] plugins have been merged. Both configuration formats are still accepted, so you only have to change 'adv_exec' to 'exec' in your config if you were using the adv_exec plugin.

=== 7.10.2010 r1486 (d.m.yyyy) ===

The manipulate plugin now has a parameter for what event the manipulate should be run in. The default event to run on has also been changed from the filter event to the metainfo event. If this causes issues with how you use manipulate, you can specify 'event: filter' for your manipulates to restore the old behavior. This is how the event setting should be defined:

{{{
manipulate:
  - series_name_dots:
      event: filter
      from: series_name
      replace:
        regexp: ' '
        format: '.'
}}}

=== 8.9.2010 r1395 (d.m.yyyy) ===

Changes to [wiki:Plugins/manipulate manipulate] plugin configuration. Now accepts a list of single item dicts, see plugin page for details. ([wiki:Cookbook/Series/DelugeSeriesLabel?action=diff&version=3 example config diff])

=== 13.6.2010 r1294 (d.m.yyyy) ===

[wiki:Plugins/exists_series exists_series] no longer allows multiple qualities by default. See plugin page for details.

=== 11.05.2010 r1278 (d.m.yyyy) ===

Changes to [wiki:Plugins/manipulate manipulate] plugin configuration. Simply replace `regexp` with `extract`.

=== 05.04.2010 r1226 (d.m.yyyy) ===

Plugins `torrent_size` and `nzb_size` have been merged into one [wiki:Plugins/content_size content_size].

=== 26.03.2010 r1211 (d.m.yyyy) ===

New dependency, subversion users should run install progressbar (eg. `bin/easy_install progressbar`)

=== 15.02.2010 r1119 (d.m.yyyy) ===

This release was packed incorrectly and will complain about duplicate plugins, please upgrade to r1120.

=== 12.02.2010 r1115 (d.m.yyyy) ===

Subversion users need to delete all `.pyc` files from `flexget/plugins/`. You can also try `bin/paver clean_compiled` if that does it for you.

=== 18.01.2010 (d.m.yyyy) ===

For all old users, execute:

{{{
sqlite3 db-config.sqlite "create index seen_values_index on seen (value);"
}}}

This will improve execution speeds.

=== 27.12.2009 r1042 (d.m.yyyy) ===

Presets are now defined under `presets` (like `feeds`). Update your configs!

Before:

{{{
movies:
  ...

feeds:
  ...
}}}

After:

{{{
presets:
  movies:
    ...

feeds:
  ...
}}}

=== 11.11.2009 r948 (d.m.yyyy) ===

Fixed bug that caused database to be created in current path or in flexget binary path. If you're unlucky old user and the database is located in these locations you get a message asking to verify creating new database with `--initdb`. Instead of doing this move the `db-config.sqlite` file to same path as where your configuration file is.

'''Note:''' `--initdb´ was later removed so you might not get this alert if you upgrade from older than r948 straight to latest version, if you get fresh database and you'd rather maintain old history please find the incorrectly placed database and move it to same path as where your configuration file is.

=== 02.11.2009 ===

If you managed to add `None` into `--imdb-queue` you can use this to delete it.

{{{
sqlite3 db-config.sqlite "delete from imdb_queue where imdb_id is NULL;"
}}}

=== 23.10.2009 r862 (d.m.yyyy) ===

Renamed `directories` to `listdir`. Update your configs.

=== 6.10.2009 (d.m.yyyy) ===

'''Action required when upgrading'''

 * From svn prior to r781
 * From beta egg prior to beta 7

While in beta, no automatic database migration is provided so once in a while change comes along that requires user actions.

Please execute following:

{{{
sqlite3 db-config.sqlite "drop table series; drop table series_episodes; drop table episode_qualities;"
}}}

Then run !FlexGet once with {{{--learn}}} to make sure no series will be re-downloaded.

=== Subversion users: r663 - dependency changes ===

If upgrading to this, run:

{{{
bin/paver clean
python bootstrap.py
}}}

=== Subversion users: r661 - setup tools / pavement ===

After updating to this revision you need to run:

{{{
python bootstrap.py
}}}

If you get error about !BeautifulSoup add parameter {{{--no-site-packages}}}

!FlexGet executable has also been relocated, it is now in:

{{{
bin/flexget
}}}

Edit your cron to new location:

{{{
~/(install path)/bin/flexget -q
}}}