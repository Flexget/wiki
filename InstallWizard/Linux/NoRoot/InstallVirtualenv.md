= Install virtualenv =

== Download ==

Download the `tarball` from:

http://pypi.python.org/pypi/virtualenv

Extract it:

{{{
tar xvfz virtualenv-tip.gz
}}}

You can't install the package with the included `setup.py`, but you can still use it just fine.

== Create environment ==

Extracted directory has python executable, let's put it into use.

{{{
python virtualenv.py ~/flexget/
cd ~/flexget/
}}}

Now you have created isolated python environment (virtualenv).

To activate the virtualenv, run command:

{{{
source ~/flexget/bin/activate
}}}

Now your `python` and `easy_install` commands will use this environment.

== Continue ==

[wiki:InstallWizard/Linux/NoRoot/InstallVirtualenv/FlexGet Install FlexGet]
