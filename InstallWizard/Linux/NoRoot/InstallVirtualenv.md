= Install virtualenv =

=== Download ===

Download the virtualenv `tarball` from:

http://pypi.python.org/pypi/virtualenv

Extract it:

{{{
tar xvfz virtualenv-tip.gz
}}}

You can't install the package with the included `setup.py`, but you can still use the `virtualenv.py` in it.

=== Create the environment ===

{{{
python virtualenv.py ~/flexget/
}}}

Now you have created isolated python environment (virtualenv).

To activate the virtualenv, run command:

{{{
source ~/flexget/bin/activate
}}}

Now your `python` and `easy_install` commands will use this environment, instead the one you possibly had earlier.

== Continue ==

[wiki:InstallWizard/Linux/NoRoot/InstallVirtualenv/FlexGet Install FlexGet]
