---
import:
  - FlexgetCurrentPythonRequirements
---

# Installing FlexGet on Windows

<div class="alert alert-warning" role="alert">

FlexGet is currently mostly command line based, although we have an experimental [Web UI](/Web-UI) under development. Be aware that this is not "double click to install and a beautiful UI pops up". But it's not that hard either. [Help is available.](/NeedHelp)</div>

<div class="alert alert-info" role="alert">

If you plan on using the [deluge](/Plugins/deluge) plugin on Windows, you must make sure your Deluge python version matches your system python version. [Read more here.](/Plugins/deluge#WindowsUsers)
</div>

## Set up environment

### Install Python
Supported versions of Python:
{{> FlexgetCurrentPythonRequirements }}


If you already have a compatible version of Python installed, you can continue to the next step.

Otherwise, install the latest version of Python 2.7 or a compatible version of 3.x (see supported versions list above) from [python.org](http://python.org/download/).

### Verify Python is in your PATH

The Python installer should put the Python interpreter into your [PATH](http://en.wikipedia.org/wiki/Environment_variable#System_path_variables) environment variable. You can test this by opening a command prompt and running this command:
```bash
python -V
```

If anything happens other than displaying the version of Python that is installed, it's not in your PATH.

[ComputerHope](https://www.computerhope.com/issues/ch000549.htm) has a good article on how to change your PATH. Note that you want to *add* to your path, *not replace it*, or other things on your system might stop working.

### Install/Upgrade pip
<!-- https://sites.google.com/site/pydatalog/python/pip-for-windows
pipwin is broken as of September 2016 - setuptools moved to Github and pipwin is still trying (as of May 2017) to access the old bitbucket.org URL -->

#### Installing
pip is included with Python as of v2.7.9 and v3.4.

If you must use a prior version of Python, you can install PIP using the instructions found [here](https://packaging.python.org/installing/#install-pip-setuptools-and-wheel):

- Download [get-pip.py](https://bootstrap.pypa.io/get-pip.py).
- In a command prompt, run `python get-pip.py`. This will install or upgrade pip. Additionally, it will install setuptools and wheel if they’re not installed already.

#### Upgrading
If your version of Python came with pip, you still need to ensure it's upgraded to the latest version. Open a command prompt and run this command:

```bash
python -m pip install -U pip setuptools
```

This will upgrade PIP and setuptools to the latest versions.

### Continue
After successfully installing *Python* and *pip*, continue to [Install FlexGet](/InstallWizard/Windows/FlexGet).
