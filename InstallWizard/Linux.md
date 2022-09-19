---
title: Linux
description: 
published: true
date: 2022-09-18T05:23:40.104Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:12.084Z
---

# Linux/BSD
## Prerequisites

### Python

Supported versions of Python:
[FlexgetCurrentPythonRequirements](/FlexgetCurrentPythonRequirements){.include}


You can check your installed version of Python with this command:

```bash
python -V
```

It's also worth trying `python3` and/or hitting tab for autocomplete in case you already have python 3 installed, which is often the case.

Example of installation in a Debian-based system:

```bash
sudo apt-get install python3.8
```

## Create virtualenv

Python virtualenvs provide isolated python runtime. It does not mess with your operating system and can be easily deleted and recreated if needed.

### Python 3

Python3 generally ships with virtualenv. Simply run:

```bash
python3 -m venv ~/flexget/
```

If this does not work (eg. on ubuntu) you may need to install virtualenv package with:

```bash
sudo apt install python3-venv
```

## Upgrade virtualenv tools

Virtualenv is very likely created with old versions of some necessary tools and this can fail the installation or FlexGet may seem broken after installation. Please upgrade them with:

```bash
~/flexget/bin/pip install --upgrade pip setuptools
```

## Install FlexGet in the `virtualenv`

```bash
~/flexget/bin/pip install flexget
```

This will install FlexGet and all of it's dependencies.

## Running FlexGet from the `virtualenv`

The `virtualenv` can be activated with this command:

```bash
source ~/flexget/bin/activate
```

After activation, the command `flexget` will work from anywhere. Note that activation does not persist over to new shell sessions.

Alternatively you can use following command without activating `virtualenv`.

```bash
~/flexget/bin/flexget [options]
```

You will need to use this form if you use crontab to schedule FlexGet executions.

## Alternatively - Install globally

Not generally recommended. Global install for all users can be achieved with the following command. This requires `pip` to be available for root.

```bash
sudo pip install flexget
```

This usually works fine, but in some cases you may run into issues if multiple Python packages request different versions of libraries. `virtualenv` does not suffer from this issue and is the recommended method for new users.

## Next Step

Continue to [Scheduling](/InstallWizard/Linux/Scheduling).