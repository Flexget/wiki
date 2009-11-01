= Bleeding edge users information =

Important notes for 1.0 / bleeding edge users:

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

If {{{sqlite3}}} command is not available, try installing relevant tool packages (ie. apt-get install sqlite3). If all else fail deleting database and running {{{--learn}}} will fix database but may cause some older items to be re-downloaded if they appear in the feed again.

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