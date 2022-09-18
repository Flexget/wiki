---
title: Python
description: 
published: true
date: 2022-09-18T05:23:54.522Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:23:51.904Z
---

# [Install Wizard](/InstallWizard) > [OSX](/InstallWizard/OSX) > Python and pip

<div class="alert alert-info" role="alert">
<span class="glyphicon glyphicon-info-sign"></span>
&nbsp;The instructions in this step assume you have just installed Homebrew as detailed on the <a href="/InstallWizard/OSX">previous page</a>. There are also instructions available <a href="/InstallWizard/OSX/OtherMethods">for other methods</a> of installing Python, pip, and Flexget.
</div>

## Python and pip
Next you will need to install Python and pip. These versions of Python are currently supported:
{{> FlexgetCurrentPythonRequirements }}


Homebrew will install the latest version of Python 3, and pip alongside it.

```bash
# installs the latest version of Python 3.x
$ brew install python
```

Once Python is installed, you can test it by running this command:
```bash
python -V
```
It should output either v3.7.5 or higher. If it's a lower version, you probably didn't update your `PATH` correctly and it's still using the system-installed version.

By installing Python using Brew, you also installed pip and setuptools. If you installed Python 3, replace the `pip` command going forward with `pip3`.

You should upgrade pip to the latest version, as well as setuptools:
```bash
# upgrade pip and setuptools (Python 3.x)
$ pip3 install --upgrade pip
$ pip3 install --upgrade setuptools
```

## Continue

On the next page learn how to [install FlexGet](/InstallWizard/OSX/Flexget) itself.