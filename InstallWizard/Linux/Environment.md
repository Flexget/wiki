= Set up environment =

== Python ==

Start by making sure you have Python '''2.5.x - 2.7.x''' available. Try running commands:

{{{
python -V
}}}

In some distributions the newer python may be available trough commands:

{{{
python25 -V
python26 -V
python27 -V
}}}

If you don't have required version already available, install it from your distribution package manager.

With Debian based distributions you can simply run:

{{{
sudo apt-get install python2.6
}}}

== easy_install ==

If you do not have `easy_install` already available, you need to install it.

With Debian based distributions you can simply run with root privileges:

{{{
sudo apt-get install python-setuptools
}}}

If your distribution does not have the package available, see further instructions from 

[http://pypi.python.org/pypi/setuptools]

= Next =

[wiki:InstallWizard/Linux/Environment/FlexGet Install FlexGet]