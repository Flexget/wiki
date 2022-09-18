---
title: OSX
description: 
published: true
date: 2022-09-18T05:23:55.849Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:15.886Z
---

# [Install Wizard](/InstallWizard) > OSX

<div class="container-fluid alert alert-warning">
  <div class="row text-center">
    <div class="col-sm-1 col-md-1 col-lg-1">
      <span class="glyphicon glyphicon-exclamation-sign fa-2x"></span>
    </div>
    <div class="col-sm-11 col-md-11 col-lg-11 text-left">
      macOS (previously called OS X) ships with a version of Python installed, but it is usually not the latest version, and installing additional packages against the system version is not recommended. If you don't already have a separate Python installation, the easiest and safest way is to install a separate copy of Python for use with FlexGet.
    </div>
  </div>
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

Add this at the bottom by using your arrow keys to navigate and pasting it on a new line.
```bash
export PATH="/usr/local/bin:/usr/local/sbin:~/bin:$PATH"
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