# Installing FlexGet on Windows
**NOTE:** If you plan on using the [deluge](/Plugins/deluge) plugin on Windows, you must make sure your Deluge python version matches your system python version, [read more.](/Plugins/deluge#WindowsUsers)

## Set up environment
If you already have python 2.7, 3.3 or newer and pip, you can continue to next step.

### Install Python
Install latest python 2.7 or latest 3.x from [python.org](http://python.org/download/). 

### Install PIP
https://sites.google.com/site/pydatalog/python/pip-for-windows

Since this might not put pip in your [PATH](http://en.wikipedia.org/wiki/Environment_variable#System_path_variables) environment variable you will have to either add it there or use full path to the command (meaning c:\Python27\Scripts\pip instead of plain pip).

If you are having trouble with the windows installer version of pip 1.4, an alternative is to run 'easy_install pip' to install it via python. (if you don't have python in your path easy_install can be found in c:\Python27\scripts

## Continue
After successfully installing *Python* and *pip*

[Install FlexGet](/InstallWizard/Windows/FlexGet)
