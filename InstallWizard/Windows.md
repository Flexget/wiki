= Installing !FlexGet on Windows =

This is unnecessarily complicated at the moment, easier methods for installing are planned.

'''NOTE:''' If you plan on using the [wiki:Plugins/deluge deluge] plugin on Windows, you must make sure your Deluge python version matches your system python version, [wiki:Plugins/deluge#WindowsUsers read more.]

== Set up environment ==

If you already have '''Python 2.6.x - 2.7.x''' and '''pip''', you can continue to next step.

=== Install Python ===

Install latest '''Python 2.7.x''' from [http://python.org/download/ python.org]. Like many other python applications today, !FlexGet is '''not''' compatible with new Python 3.x.

=== Install pip ===

https://sites.google.com/site/pydatalog/python/pip-for-windows

Since this might not put pip in your [http://en.wikipedia.org/wiki/Environment_variable#System_path_variables PATH] environment variable you will have to either add it there or use full path to the command (meaning c:\Python2X\Scripts\pip instead of plain pip).

If you are having trouble with the windows installer version of pip 1.4, an alternative is to run 'easy_install pip' to install it via python. (if you don't have python in your path easy_install can be found in c:\Pythonx\scripts where x is the version of python you have installed (normally 2.6 so c:\Python26\scripts))

== Continue ==

After successfully installing ''Python'' and ''pip''

[wiki:InstallWizard/Windows/FlexGet Install FlexGet]
