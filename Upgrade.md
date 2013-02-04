= Upgrading 1.0 installation =

If you're still using 0.9 see [wiki:MigrateTo10 this].

== Check current version ==

'''''[[Include(http://download.flexget.com/latestversion)]]'''''

Start by checking what version you currently have with command:

{{{
flexget -V
}}}

'''''Git Users:''''' You can check the latest release you have by getting new tags with {{{git fetch --tags}}} then running {{{git describe}}}

Write this down somewhere.

== Upgrade ==

If you have short cron interval, comment !FlexGet out from the cron. After you've ran successfully manually, put it back.

{{{
pip install --upgrade flexget
}}}

[wiki:PipProblems Problems with pip?]

Git users can just run `git pull`.

== Verify ==

Check if your configuration file is still valid, there may have been some changes to it.

{{{
flexget --check
}}}

If your configuration doesn't pass check, Have a look at [wiki:UpgradeActions upgrade actions] to see if there are any actions you must take. The behavior of certain plugins may also have changed, so check [wiki:UpgradeActions upgrade actions] even if your config is passing.

For example, if you were running r904 follow all the steps above this revision.

=== Problems ? ===

If you encounter problems, there are ways to get [wiki:NeedHelp help] !

Start by removing traces of old !FlexGet from your python site-packages, eg.

{{{
rm /usr/local/lib/python2.6/site-packages/FlexGet-1.0r1108-py2.6.egg
}}}

If you receive errors about database upgrades please report them via a [http://flexget.com/newticket ticket]. If you do not care about the history for that plugin, you can reset the database for that plugin with {{{--reset-plugin PLUGINNAME}}} to get it working again.