= Upgrading 1.0 installation =

If you're still using 0.9 see [wiki:MigrateTo10 this].

== Check current version ==

Start by checking what version you currently have with command:

{{{
flexget -V
}}}

'''TODO:''' Some way for git users to figure which build they have.

Write this down somewhere.

== Upgrade ==

If you have short cron interval, comment !FlexGet out from the cron. After you've ran successfully manually, put it back.

{{{
pip install --upgrade flexget
}}}

[wiki:PipProblems Problems with pip?]

Subversion users can just run `svn up`.

== Verify ==

Check if your configuration file is still valid, there may have been some changes to it.

{{{
flexget --check
}}}

If your configuration doesn't pass check, Have a look at [wiki:UpgradeActions upgrade actions] to see if there are any actions you must take. 

For example, if you were running r904 follow all the steps from this revision upwards.

=== Problems ? ===

If you encounter problems, there are ways to get [wiki:NeedHelp help] !

Start by removing traces of old !FlexGet from your python site-packages, eg.

{{{
rm /usr/local/lib/python2.6/site-packages/FlexGet-1.0r1108-py2.6.egg
}}}

If you receive errors about database upgrades please report them via a [http://flexget.com/newticket ticket]. If you do not care about the history for that plugin, you can reset the database for that plugin with {{{--reset-plugin PLUGINNAME}}} to get it working again.
