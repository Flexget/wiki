= !FlexGet subversion =

== Checkout from SVN ==

If you're familiar with subversion you can use it to make upgrading etc more easily.

For stable release you should checkout from 0.9 branch which is kept stable.

{{{
svn co http://svn.flexget.com/branches/0.9 flexget-0.9
}}}

Only ''bleeding edge'' users should checkout from trunk.

{{{
svn co http://svn.flexget.com/trunk flexget-dev
}}}

== Update from SVN ==

Enter path where you did checkout and run

{{{
svn update
}}}

If you're interested improving !FlexGet or maintaining (new) modules, please [wiki:NeedHelp contact] for write access! Patches are also very much welcomed, just create new ticket with description and attach the patch file.
