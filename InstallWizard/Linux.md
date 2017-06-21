---
import:
  - FlexgetCurrentPythonRequirements
---

# Linux/BSD
## Prerequisites

### Python

Supported versions of Python:
{{> FlexgetCurrentPythonRequirements }}


You can check your installed version of Python with this command:

```bash
python -V
```

Example of installation in a Debian-based system:

```bash
sudo apt-get install python3.5
```

Example of installation in an Arch-based system:

```bash
sudo pacman -S python2
```

**NOTE:** Deluge doesn't support Python 3.x yet. Stick with Python 2.7 if you plan to use it.

### PIP

The next piece of required software is the Python package manager called PIP. This can be usually found from your operating system's package repository under the name `python-pip` or `python3-pip`. If you install `python3-pip` it may need to be used via the command `pip-3.5` or something similar.

Example of installation in a Debian-based system:

```bash
sudo apt-get install python-pip
```

Example of installation in an Arch-based system:

```bash
sudo pacman -S python2-pip
```

## Upgrade setuptools

Using the latest setuptools will save headaches. This can be achieved with the following command:

```bash
sudo pip install --upgrade setuptools
```

## Install in a `virtualenv`

This is the recommended way to install FlexGet, unless you want multiple accounts in the system to be able to use FlexGet without each having to install it themselves.

Install virtualenv with this command:

```bash
sudo pip install virtualenv
```

### Create the `virtualenv`

This creates an isolated Python environment. You can create as many of these as you like for each Python application you use.

```bash
virtualenv ~/flexget/
```

**NOTE:** If you plan to use the [deluge](/Plugins/deluge) plugin, you need to build your virtualenv with the --system-site-packages option so that the deluge package is available to FlexGet.

```bash
virtualenv --system-site-packages ~/flexget/
```

### Install FlexGet in the `virtualenv`

```bash
cd ~/flexget/
bin/pip install flexget
```

This will install FlexGet and all of it's dependencies.

### Running FlexGet from the `virtualenv`

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

Global install for all users can be achieved with the following command. This is also somewhat easier than to use a `virtualenv`.

```bash
sudo pip install --upgrade setuptools
sudo pip install flexget
```

This usually works fine, but in some cases you may run into issues if multiple Python packages request different versions of libraries. `virtualenv` does not suffer from this issue and is the recommended method for new users.

## Next Step

Continue to [Scheduling](/InstallWizard/Linux/Scheduling).