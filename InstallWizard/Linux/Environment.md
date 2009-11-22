= Setup environment =

== Python ==

Start by making sure you have Python 2.5.x or Python 2.6.x available. Try running command:

{{{
python -V
}}}

If you don't have required version already available, install it from the distribution package manager.

With Debian based distributions you can simply run with root privileges:

{{{
apt-get install python2.6
}}}

== easy_install ==

If you do not have `easy_install` already available, you need to install it.

With Debian based distributions you can simply run with root privileges:

{{{
apt-get install python-setuptools
}}}

If your distribution does not have the package available, see further instructions from 

[http://pypi.python.org/pypi/setuptools]

= Next =

[wiki:InstallWizard/Linux/Egg Continue installation]