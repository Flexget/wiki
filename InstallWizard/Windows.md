# Installing FlexGet on Windows

<div class="alert alert-warning" role="alert">

FlexGet is currently mostly command line based, although we have experimental webui under development. Be aware that this is not double click install and beautiful UI pops up. But it's not that hard either. [Help is available.](/NeedHelp)</div>

<div class="alert alert-info" role="alert">

If you plan on using the [deluge](/Plugins/deluge) plugin on Windows, you must make sure your Deluge python version matches your system python version, [read more.](/Plugins/deluge#WindowsUsers)
</div>

## Set up environment

### Install Python
If you already have python 2.7, 3.3 or newer and pip, you can continue to next step.

Install latest python 2.7 or latest 3.x from [python.org](http://python.org/download/). 

### Install PIP
https://sites.google.com/site/pydatalog/python/pip-for-windows

Since this might not put pip in your [PATH](http://en.wikipedia.org/wiki/Environment_variable#System_path_variables) environment variable you will have to either add it there or use full path to the command (meaning c:\Python27\Scripts\pip instead of plain pip). Updating PATH to include python scripts is highly recommended for conveniency.

If you are having trouble with the windows installer version of pip 1.4, an alternative is to run `easy_install pip` to install it via python. 

### Continue
After successfully installing *Python* and *pip*

[Install FlexGet](/InstallWizard/Windows/FlexGet)
