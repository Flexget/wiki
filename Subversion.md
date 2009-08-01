= !FlexGet subversion =

== Checkout from SVN ==

If you're familiar with subversion you can use it to make upgrading etc more easily.

For stable release you should checkout from 0.9 branch which is kept stable.

{{{
svn co http://svn.flexget.com/branches/0.9 flexget-0.9
}}}

=== Bleeding edge (upcoming 1.0) ===

'''Notes:''' 

 * Requires Python 2.5 or 2.6
 * This is under development at the moment

To checkout use command:

{{{
svn co http://svn.flexget.com/trunk flexget-dev
}}}

After checkout is complete, you need to initialize the environment.

{{{
python bootstrap.py
}}}

If you get error about !BeautifulSoup add parameter {{{--no-site-packages}}}

Now !FlexGet should be executable via:

{{{
bin/flexget
}}}

When updating remember to check [wiki:BleedingEdge bleeding edge news] in case there are changes that require actions.

== Update from SVN ==

Enter path where you did checkout and run

{{{
svn update
}}}

If you're interested improving !FlexGet or maintaining (new) modules, please [wiki:NeedHelp contact] for write access! Patches are also very much welcomed, just create new ticket with description and attach the patch file.
