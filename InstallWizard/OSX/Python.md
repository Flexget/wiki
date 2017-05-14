---
import:
  - FlexgetCurrentPythonRequirements
---

# [Install Wizard](/InstallWizard) > [OSX](/InstallWizard/OSX) > Python and pip

<div class="alert alert-warning" role="alert">

The instructions in this step assume you have just installed Homebrew as detailed on the [previous page](/InstallWizard/OSX). There are also instructions [for other methods](/InstallWizard/OSX/OtherMethods) of installing Python, pip, and Flexget.</div>

## Python and pip
Next you will need to install Python and pip. These versions of Python are currently supported:
{{> FlexgetCurrentPythonRequirements }}


Homebrew will install the latest version of Python 2.7.x or 3, and pip alongside it. As of this writing, Python 3.6 is not supported by FlexGet, so if you want to install Python 3, you must run the specific command below to install v3.5.2 *and not* the normal Python 3 Brew command.

```bash
# installs the latest version of Python 2.x
$ brew install python

# installs Python 3.5.2
$ brew install https://raw.githubusercontent.com/Homebrew/homebrew-core/ec545d45d4512ace3570782283df4ecda6bb0044/Formula/python3.rb
```

Once Python is installed, you can test it by running this command:
```bash
python -V
```
It should output either v2.7.13 or higher, or v3.5.2. If it's a lower version, you probably didn't update your `PATH` correctly and it's still using the system-installed version.

By installing Python using Brew, you also installed pip and setuptools. If you installed Python 3, replace the `pip` command going forward with `pip3`.

You should upgrade pip to the latest version, as well as setuptools:
```bash
# upgrade pip and setuptools (Python 2.x)
$ pip install --upgrade pip
$ pip install --upgrade setuptools

# upgrade pip and setuptools (Python 3.x)
$ pip3 install --upgrade pip
$ pip3 install --upgrade setuptools
```

## Continue

On the next page learn how to [install FlexGet](/InstallWizard/OSX/Flexget) itself.