= !FlexGet subversion =

== Checkout from SVN ==

If you're familiar with subversion and want to stay in bleeding edge you can checkout directly from development repository.

{{{
svn co http://svn.flexget.com/trunk flexget-dev
}}}

For more stable release you may wish to checkout from branch 0.9 which will be in more stable mode until 1.0 is released. After 1.0 release this branch will no longer be updated.

{{{
svn co http://svn.flexget.com/branches/0.9 flexget-0.9
}}}

== Update from SVN ==

Enter path where you did checkout and run

{{{
svn update
}}}

If you're interested improving !FlexGet or maintaining (new) modules, please [wiki:NeedHelp contact] for write access! Patches are also very much welcomed, just create new ticket with description and attach the patch file.
