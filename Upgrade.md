= Upgrading =

== Check current version ==

'''''[[Include(http://download.flexget.com/latestversion)]]'''''

Start by checking what version you currently have with command:

{{{
flexget -V
}}}

'''''Git Users:''''' You can check the latest release you have by getting new tags with {{{git fetch --tags}}} then running {{{git describe}}}

Write this down somewhere.

== Backup database(s) (optional) ==

In case you wish to roll back to previous version you will need to make backup of your database since running new version will upgrade it and downgrade is not supported.

Each configuration file has corresponding database file, so for example config.yml will have db-config.sqlite

Copy this file to backup file containing the version number you are were last using, e.g. db-config.sqlite_1.1.59

== Upgrade ==

If you have short cron interval, comment !FlexGet out from the cron. After you've ran successfully manually, put it back. If you are running the daemon, you should stop the daemon until the upgrade is complete and you verify your config file works with the updated version.

{{{
pip install --upgrade flexget
}}}

[wiki:PipProblems Problems with pip?]

Git users can just run `git pull`. If the dependencies have changed, you'll also have to run `bootstrap.py` again to upgrade them.

== Verify ==

Check if your configuration file is still valid, there may have been some changes to it.

{{{
flexget check
}}}

If your configuration doesn't pass check, Have a look at [wiki:UpgradeActions upgrade actions] to see if there are any actions you must take. The behavior of certain plugins may also have changed, so check [wiki:UpgradeActions upgrade actions] even if your config is passing.

For example, if you were running 1.1.2 follow all the steps above this revision.

=== Problems ? ===

If you encounter problems, there are ways to get [wiki:NeedHelp help] !

Start by removing traces of old !FlexGet from your python site-packages, eg.

{{{
rm /usr/local/lib/python2.6/site-packages/FlexGet-*
}}}

Also make sure you are running the latest package of pip.

{{{
pip install --upgrade pip
}}}

Special note for Arch Linux users. Yours is different.
{{{
pip2 install --upgrade pip
}}}

If you receive errors about database upgrades please report them via a [http://flexget.com/newticket ticket]. If you do not care about the history for that plugin, you can reset the database for that plugin with {{{--reset-plugin PLUGINNAME}}} to get it working again.