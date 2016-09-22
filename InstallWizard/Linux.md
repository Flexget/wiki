# Linux/BSD
## Prerequisites

Let's make sure you have necessary software installed.

### Python

FlexGet requires Python 2.7, 3.3 or newer to run. You can check your version with command.

```bash
python -V
```

Example in Debian based system:

```bash
sudo apt-get install python3.5
```

Example in Arch based system:

```bash
sudo pacman -S python2
```

**Note:** Deluge doesn't support Python 3.x yet. Stick with Python 2.7 if you plan to use it.

### PIP

Second piece of required software is python package manager called PIP. This can be usually found from operating system package repository under name `python-pip` or `python3-pip`. If you install `python3-pip` it may need to be used via command `pip-3.5` or something similar.

Example in Debian based system:

```bash
sudo apt-get install python-pip
```

Example in Arch based system:

```bash
sudo pacman -S python2-pip
```

## Upgrade setuptools

Using latest setuptools will save headaches in some older installations, this can be achieved with.

```bash
sudo pip install --upgrade setuptools
```

## Install in a virtualenv

This is the recommended way unless you want multiple accounts in the system to be able to use FlexGet without each having to install it themselves.

### Install virtualenv

```bash
sudo pip install virtualenv
```

### Create virtualenv

This creates isolated python environment. You can create as many of these as you like for each python application you use.

```bash
virtualenv ~/flexget/
```

**Note:**  if you plan to use the [deluge](/Plugins/deluge) plugin, you need to build your virtualenv with the --system-site-packages option.

```bash
virtualenv --system-site-packages ~/flexget/
```

### Install FlexGet in the virtualenv

```bash
cd ~/flexget/
bin/pip install flexget
```

This will install FlexGet and all it's dependencies.

### Running FlexGet from the virtualenv

Virtualenv can be activated with command:

```bash
source ~/flexget/bin/activate
```

After activation command `flexget` will work from anywhere. Note that activation does not persist over to new shell sessions.

Alternatively you can use following command without activating virtualenv.

```bash
~/flexget/bin/flexget [options]
```

You will need to use this form if you use crontab to schedule FlexGet executions.

## Install globally

Global install for all users can be achieved with the following command. This is also somewhat easier than to mess with virtualenvs.

```bash
sudo pip install flexget
```

This works fine usually, but on some cases you may run into issues if multiple python packages request different versions of libraries. Virtualenv does not suffer from this issue.

## Next step?

Continue to [Scheduling](/InstallWizard/Linux/Scheduling)