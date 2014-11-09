= !FlexGet !GitHub install =

'''Notes:''' 

 * Requires '''Python 2.6 - 2.7''', virtualenv, and git client
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

Initialize a virtualenv in your checkout directory:

{{{
virtualenv ~/flexget-dev
}}}

Once the virtualenv has been created, we need to install our checked out !FlexGet inside it. Make sure you are using the pip installed in your virtualenv by either activating the virtualenv first, or explicitly calling `bin/pip` as shown below. The `-e` flag to pip says this should be an editable install, meaning it uses the files directly in the checkout rather than installing a package in site-packages.

{{{
cd ~/flexget-dev
bin/pip install -e .
}}}

Once this is completed you'll have !FlexGet installed in a virtualenv.

You can execute !FlexGet via:

{{{
~/flexget-dev/bin/flexget
}}}

== Become a contributor ==

If you're interested improving !FlexGet or maintaining (new) plugins, please read [wiki:Contribute contribute page].
