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

It's also worth trying `python3` and/or hitting tab for autocomplete in case you already have python 3 installed, which is often the case.

Example of installation in a Debian-based system:

```bash
sudo apt-get install python3.5
```

### Python 2.7 virtualenv (legacy)

We no longer recommend or provide detailed instructions for Python 2.7 as it is going to be retired at the end of 2019. It is highly recommended to proceed with Python 3 based environment. To install Python 2.7 based system you will need to install pip and virtualenv then create virtual environment and follow instructions from there. On debian this would be something like this:

```bash
sudo apt-get install python-pip
sudo pip install virtualenv
virtualenv ~/flexget/
```

### Python 3 virtualenv

Python3 ships with virtualenv. Simply run:

```bash
python3 -m venv ~/flexget/
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

Not generally recommended. Global install for all users can be achieved with the following command. This requires `pip` to be available for root.

```bash
sudo pip install flexget
```

This usually works fine, but in some cases you may run into issues if multiple Python packages request different versions of libraries. `virtualenv` does not suffer from this issue and is the recommended method for new users.

## Next Step

Continue to [Scheduling](/InstallWizard/Linux/Scheduling).