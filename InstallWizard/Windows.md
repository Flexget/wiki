---
title: Windows
description: 
published: true
date: 2025-08-25T07:06:32.225Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:38.884Z
---

# [Install Wizard](/InstallWizard) > Windows

> FlexGet is currently mostly command line based, although we have an experimental [Web UI](/Web-UI) under development. Be aware that this is not "double click to install and a beautiful UI pops up". But it's not that hard either. [Help is available.](/NeedHelp)
{.is-warning}

## Set up environment

### Install Python
Supported versions of Python:

![](https://img.shields.io/pypi/pyversions/flexget?style=for-the-badge&logo=python&logoColor=white)

If you already have a compatible version of Python installed, you can continue to the next step.

Otherwise, install a compatible version of 3.x (see supported versions list above) from [python.org](http://python.org/download/).

### Verify Python is in your PATH

The Python installer should put the Python interpreter into your [PATH](http://en.wikipedia.org/wiki/Environment_variable#System_path_variables) environment variable. You can easily test this.

Run this program as an adminstrator: `Start Menu` &rarr; `Accessories` &rarr; `Command Prompt`. At the command prompt, copy and paste this command and press Enter:
```bash
python -V
```

If anything happens other than displaying the version of Python that is installed, Python is not in your PATH.

If you used the installer from python.org, there should be an item on the Start Menu for Python. Right-clicking on it and choosing Properties will tell you where the actual program file is located (hint: if the directory contains "Start Menu", that's the Start Menu item and not the actual program). Generally it should be in a directory named `pythonXX` where `XX` is the version, like `27` for v2.7.

You should also add the `scripts` subdirectory of your Python folder to your PATH.

The directories will look something like a set of these, depending on your version of Windows and how Python was installed. It may also be different. The important thing is that you're adding the *full directory names* for Python and the scripts folder to your PATH, not just the literal phrases `Python35` and `Scripts`.
```bash
C:\Python35
C:\Python35\Scripts

C:\Users\<username>\AppData\Local\Programs\Python\Python35
C:\Users\<username>\AppData\Local\Programs\Python\Python35\Scripts
```

[ComputerHope](https://www.computerhope.com/issues/ch000549.htm) has a good article on how to change your PATH. Note that you want to *add* to your path, *not replace it*, or other things on your system might stop working.

### Install/Upgrade pip
#### Install
Typically, Python comes with pip pre-installed. If not, you will need to install pip by following the instructions at [packaging.python.org](https://packaging.python.org/en/latest/tutorials/installing-packages/#ensure-you-can-run-pip-from-the-command-line).
#### Upgrade
Ensure `pip` is on a supported version. If not, open a command prompt and run this command:

```bash
python -m pip install -U pip setuptools
```

This will upgrade `pip` and `setuptools` to the latest versions.

### Continue
After successfully installing *Python* and *pip*, continue to [Install FlexGet](/InstallWizard/Windows/FlexGet).
