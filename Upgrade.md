= Upgrading 1.0 installation =

If you're still using 0.9 see [wiki:MigrateTo10 this].

== Check current version ==

Start by checking what version you currently have with command:

{{{
flexget -V
}}}

Subversion users must use `svnversion .` in checkout directory instead.

Write this somewhere down.

== Upgrade ==

If you have short cron interval, comment !FlexGet out from the cron. After you've ran successfully manually, put it back.

{{{
easy_install --upgrade flexget
}}}

Subversion users can just run `svn up`.

You may also need to remove old !FlexGet from your python site-packages, eg. `rm /usr/local/lib/python2.6/site-packages/FlexGet-1.0r1108-py2.6.egg`

== Necessary actions ?==

See [wiki:UpgradeActions upgrade actions] and see if there are any steps that you must do, if you have several months old version there are almost certainly some changes that need you to take some actions.

For example, if you were running r904 follow all the steps from this revision upwards. Usually this means running some sqlite3 commands or modifying configuration file.

== Verify ==

To make sure !FlexGet is working alright after upgrade, simply run.

{{{
flexget --check
}}}