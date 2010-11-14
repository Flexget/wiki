= Required upgrading actions =

Just planning upgrading? See [wiki:Upgrade upgrade guide] first!

If {{{sqlite3}}} command is not available, try installing relevant packages (ie. apt-get install sqlite3). In windows you might want to take a look at [http://sqliteman.com/ sqliteman] for executing SQL statements. If all else fail deleting the database and running {{{--learn}}} will fix it but may cause some older items to be re-downloaded if they appear in the feed(s) again.

Note: Run all sqlite3 commands from the directory where your `db-config.sqlite` file is located (eg. ~/.flexget).

In future (after official 1.0 release) manual tweaking should not be needed anymore ... (#288)

== 14.11.2010 r1639 (d.m.yyyy) ==

The transmissionrpc plugin has been renamed to [wiki:Plugins/transmission transmission]. Your config must be updated to reflect this.

== 10.11.2010 r1620 (d.m.yyyy) ==

[wiki:Plugins/exec Exec] plugin no longer escapes anything by default during string substitution. If your fields might contain something that needs escaped, you can use the [wiki:Plugins/exec?version=9#Autoescapeoption auto_escape] option to have all non word characters escaped with backslash.

== 9.11.2010 r1617 (d.m.yyyy) ==

The [wiki:Plugins/exec exec] plugin no longer tries to do any automatic quoting on string replaced variables. Instead, the values that get replaced will have any contained quotes escaped with a backslash. This means the command now gets passed as it appears in your config to the shell to be executed. If you are using a variable that may contain spaces, you have to manually add quotes around that argument in your command now. Alternatively, you may have to stop escaping quotes in your command if you were doing so to have them to have them survive the automatic quoting process. (see #800)

== 3.11.2010 r1582 (d.m.yyyy) ==

There were some changes to how the _excluding operations work when multiple regexps have been defined in the [wiki:Plugins/regexp regexp] plugin.
Before, reject_excluding would reject if an entry omitted ''all'' of the listed regexps, now it will reject if an entry omits ''any'' of the listed regexps. (same goes for accept_excluding)

For example, this config:
{{{
regexp:
  reject_excluding:
    - titleA
    - groupA
}}}
Will now reject an entry called {{{titleA.something}}} but not {{{titleA.groupB}}}

If you were using the old behavior, you can achieve the same thing by altering your regexp to be like this:
{{{
  reject_excluding:
    - titleA|groupB
}}}
Which would not reject either {{{titleA.something}}} or {{{groupB.something}}}

== 30.10.2010 r1570 (d.m.yyyy) ==

Two new qualities were added, {{{720p web-dl}}} and {{{1080p web-dl}}}. In addition, the plain {{{web-dl}}} quality has been lowered in priority. You might need to update your config to match the new [wiki:Plugins/quality#KnownQualities quality hierarchy].

== 24.10.2010 r1552 (d.m.yyyy) ==

The [wiki:Plugins/exec exec] and [wiki:Plugins/adv_exec adv_exec] plugins have been merged. Both configuration formats are still accepted, so you only have to change 'adv_exec' to 'exec' in your config if you were using the adv_exec plugin.

== 7.10.2010 r1486 (d.m.yyyy) ==

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

== 8.9.2010 r1395 (d.m.yyyy) ==

Changes to [wiki:Plugins/manipulate manipulate] plugin configuration. Now accepts a list of single item dicts, see plugin page for details. ([wiki:Cookbook/Series/DelugeSeriesLabel?action=diff&version=3 example config diff])

== 20.8.2010 r1372 (d.m.yyyy) ==

Database schema changes. Please run:

{{{
sqlite3 db-config.sqlite "ALTER TABLE imdb_queue ADD title VARCHAR;"
}}}

== 13.6.2010 r1294 (d.m.yyyy) ==

[wiki:Plugins/exists_series exists_series] no longer allows multiple qualities by default. See plugin page for details.

== 11.05.2010 r1278 (d.m.yyyy) ==

Changes to [wiki:Plugins/manipulate manipulate] plugin configuration. Simply replace `regexp` with `extract`.

== 05.04.2010 r1226 (d.m.yyyy) ==

Plugins `torrent_size` and `nzb_size` have been merged into one [wiki:Plugins/content_size content_size].

== 26.03.2010 r1211 (d.m.yyyy) ==

New dependency, subversion users should run install progressbar (eg. `bin/easy_install progressbar`)

== 15.02.2010 r1119 (d.m.yyyy) ==

This release was packed incorrectly and will complain about duplicate plugins, please upgrade to r1120.

== 12.02.2010 r1115 (d.m.yyyy) ==

Subversion users need to delete all `.pyc` files from `flexget/plugins/`

== 18.01.2010 (d.m.yyyy) ==

For all old users, execute:

{{{
sqlite3 db-config.sqlite "create index seen_values_index on seen (value);"
}}}

This will improve execution speeds.

== 03.01.2010 r1057 (d.m.yyyy) ==

Some database changes, please run:

{{{
sqlite3 db-config.sqlite "ALTER TABLE make_rss ADD rsslink VARCHAR; ALTER TABLE imdb_movies ADD photo VARCHAR;"
}}}


== 27.12.2009 r1042 (d.m.yyyy) ==

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


== 11.11.2009 r948 (d.m.yyyy) ==

Fixed bug that caused database to be created in current path or in flexget binary path. If you're unlucky old user and the database is located in these locations you get a message asking to verify creating new database with `--initdb`. Instead of doing this move the `db-config.sqlite` file to same path as where your configuration file is.

== 02.11.2009 r904 (d.m.yyyy) ==

Due database changes, users must drop download_history table.

Execute:

{{{
sqlite3 db-config.sqlite "drop table download_history;"
}}}

'''Note:''' This will lose only `--downloads` report, nothing more.

== 02.11.2009 ==

If you managed to add `None` into `--imdb-queue` you can use this to delete it.

{{{
sqlite3 db-config.sqlite "delete from imdb_queue where imdb_id is NULL;"
}}}

== 23.10.2009 r862 (d.m.yyyy) ==

Renamed `directories` to `listdir`. Update your configs.

== 6.10.2009 (d.m.yyyy) ==

'''Action required when upgrading'''

 * From svn prior to r781
 * From beta egg prior to beta 7

While in beta, no automatic database migration is provided so once in a while change comes along that requires user actions.

Please execute following:

{{{
sqlite3 db-config.sqlite "drop table series; drop table series_episodes; drop table episode_qualities;"
}}}

Then run !FlexGet once with {{{--learn}}} to make sure no series will be re-downloaded.

== Subversion users: r663 - dependency changes ==

If upgrading to this, run:

{{{
bin/paver clean
python bootstrap.py
}}}

== Subversion users: r661 - setup tools / pavement ==

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