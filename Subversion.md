= !FlexGet subversion =

'''Notes:''' 

 * Requires '''Python 2.5 - 2.7''' and subversion client
 * This is under development at the moment

To checkout use command:

{{{
svn co http://svn.flexget.com/trunk flexget-dev
}}}

After checkout is complete, you need to initialize the environment.

Make sure the {{{python}}} command uses python 2.5 - 2.6. On some systems this may be eg. {{{python2.5}}} or {{{python25}}}.

{{{
python -V
}}}

If you're running 2.5 - 2.7, continue with:

{{{
python bootstrap.py
}}}

If you get error about !BeautifulSoup or any site packages add parameter {{{--no-site-packages}}}.

Once bootstrap is completed you'll have !FlexGet installed in a virtualenv.

You can execute !FlexGet via:

{{{
bin/flexget
}}}

Experimental webui can be launched via:

{{{
bin/flexget-webui
}}}

== Become a contributor ==

If you're interested improving !FlexGet or maintaining (new) plugins, please [wiki:NeedHelp contact] for write access! Patches are also very much welcomed, just create new ticket with description and attach the patch file.
