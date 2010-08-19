= Bleeding edge users information =

Important notes for 1.0 beta / bleeding edge users:

If {{{sqlite3}}} command is not available, try installing relevant packages (ie. apt-get install sqlite3). In windows you might want to take a look at [http://sqliteman.com/ sqliteman] for executing SQL statements. If all else fail deleting the database and running {{{--learn}}} will fix it but may cause some older items to be re-downloaded if they appear in the feed(s) again.

In future (after official 1.0 release) manual tweaking should not be needed anymore ... (#288)

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