---
import:
  - FlexgetCurrentPythonRequirements
---

# [Install Wizard](/InstallWizard) > OSX

<div class="alert alert-warning clearfix" role="alert">
<div class="pull-left"><span class="glyphicon glyphicon-exclamation-sign"></span></div>
<div class="pull-right" style="display: inline-block;">macOS (previously called OS X) ships with a version of Python installed, but it is usually not the latest version, and installing additional packages against the system version is not recommended. The easiest and safest way is to install a separate copy of Python for use with FlexGet.</div>
</div>


## Homebrew
On macOS 10.10 or higher, the easiest way to install Python, pip, and FlexGet is using [Homebrew](https://brew.sh/), also known as simply Brew. (This may work on prior versions of macOS, but Homebrew is not officially supported prior to 10.10.)

First, open Terminal and install the Xcode Command Line Tools using this command:
```bash
$ xcode-select --install
```

Then install Homebrew using this command:
```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Once Homebrew has been installed, modify your PATH. Edit your `~/.profile` file:
```bash
$ nano ~/.bash_profile
```

Add this at the bottom by using your arrow keys to navigate.
```bash
$ export PATH="/usr/local/bin:/usr/local/sbin:~/bin:$PATH"
```

Press Control+X which will prompt you to save (press Y then Enter) and exit.

Run this command so your shell reflects the changes you just made:
```bash
$ source ~/.bash_profile
```

## Continue
Go to the [next page](/InstallWizard/OSX/Python) to install Python and pip.


## Other Methods
There are other methods that can be used to install Flexget, particularly on older versions of macOS. They have been moved to a separate page [available here](/InstallWizard/OSX/OtherMethods).