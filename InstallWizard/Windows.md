= Installing !FlexGet on Windows =

This is unnecessarily complicated at the moment, easier methods for installing are planned.

'''NOTE:''' If you plan on using the [wiki:Plugins/deluge deluge] plugin on Windows, you must use a specific version of Python, [wiki:Plugins/deluge#WindowsUsers read more.]

== Set up environment ==

If you already have '''Python 2.5.x - 2.6.x''' and '''easy_install''', you can continue to next step.

=== Install Python ===

Install latest '''Python 2.7.x''' from [http://python.org/download/ python.org]. Like many other python applications today, !FlexGet is '''not''' compatible with new Python 3.x.

=== Install easy_install ===

http://pypi.python.org/pypi/setuptools#downloads

'''Note:''' If you're running 64-bit windows the installer may not work. If so you will need to download [http://peak.telecommunity.com/dist/ez_setup.py ez_setup.py] and run that (eg. python ez_setup.py). This will place the easy_install executable in c:\Python2X\Scripts\.

Since this will not put easy_install in your [http://en.wikipedia.org/wiki/Environment_variable#System_path_variables PATH] environment variable you will have either add it there or use full path to the command (meaning c:\Python2X\Scripts\easy_install instead of easy_install).

== Continue ==

After successfully installing ''Python'' and ''easy_install''

[wiki:InstallWizard/Windows/FlexGet Install FlexGet]
