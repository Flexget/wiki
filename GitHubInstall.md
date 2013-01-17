= !FlexGet GitHub install =

'''Notes:''' 

 * Requires '''Python 2.6 - 2.7''' and git client
 * This where we develop

To checkout use command:

{{{
git clone https://github.com/Flexget/Flexget.git ~/flexget-dev
}}}

^You can use whatever you like in place of ~/flexget-dev^

After checkout is complete, you need to initialize the environment.

Make sure the {{{python}}} command uses python 2.6 - 2.7. On some systems this may be eg. {{{python2.7}}} or {{{python27}}}.

{{{
python -V
}}}

If you're running 2.6 - 2.7, continue with:

{{{
cd ~/flexget-dev/
python bootstrap.py
}}}

Once bootstrap is completed you'll have !FlexGet installed in a virtualenv.

You can execute !FlexGet via:

{{{
~/flexget-dev/bin/flexget
}}}

Experimental webui can be launched via:

{{{
~/flexget-dev/bin/flexget-webui
}}}

== Become a contributor ==

If you're interested improving !FlexGet or maintaining (new) plugins, please read [wiki:Contribute contribute page].
