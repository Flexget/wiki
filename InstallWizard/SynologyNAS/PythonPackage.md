---
title: PythonPackage
description: 
published: true
date: 2022-09-18T05:24:10.463Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:24:07.782Z
---

# [Install Wizard](/InstallWizard) > [SynologyNAS](/InstallWizard/SynologyNAS) > PythonPackage

## Before We Begin

> FlexGet supports Python 3.6-3.8
{.is-warning}

The Python installation available in DSM’s Package Center provides Python 3.5.1, and as such, is not compatible with current releases of FlexGet. As a result, the current recommendation is to uninstall Python and Python 3 from the DSM Package Center, and to use Entware-NG’s opkg source instead.

While not technically required, there are a couple of highly useful application packages that will make your life easier if you are not a Linux expert. [Config File Editor](www.mertymade.com/pkg/20110919/ConfigFileEditor-noarch-14.spk) is a basic text editor for your Synology config files, and is extremely useful for maintaining configuration files. It can be used to edit your FlexGet configuration file, and is also great for editing your startup files for Entware services to begin running at boot.

NOTE: Config File Editor requires you to be logged in to the “admin” account to use it, which many users have disabled. You can follow the [instructions here](https://community.synology.com/enu/forum/17/post/56615?page=5&sort=oldest) to fix this issue if you want to use it with other accounts.

You will need to use `ssh` or `telnet` to access your server for this guide. To ensure `ssh/telnet` is enabled, go to the `Control Panel` on your Synology NAS, go to `Terminal & SNMP`, and check the box to enable the service you choose. SSH is recommended for security.


## Install Entware-ng

Go to the [Entware Github installation page](https://github.com/Entware/Entware-ng/wiki/Install-on-Synology-NAS) and follow the instructions to install Entware onto your system.

Please note that for Synology DSM 6.0 and greater, your startup script should be placed in Task Scheduler as a triggered task under the root user for best results, and run at boot. You can use Config File Editor to modify the `/etc/profile` file (DSM 6.0 and above) to add `/opt/bin` and `/opt/sbin` to the `PATH` variable for interactive login.

Reboot your NAS once Entware is installed.


## Install Required Dependencies

Now that we have Entware installed, we can use opkg commands to install Python, pip, setuptools, and gcc. These are required in order to install and use FlexGet on Synology.
```
$ sudo su
$ opkg install python3
$ opkg install python3-dev
$ opkg install python3-pip
$ opkg install gcc
```

With your dependencies installed, we’re going to make a couple modifications to make things easier on us in the future. To begin, we’re going to link our python 3 installation to the main python folder. If you initially had python 2.X or a previous version of python, this will also eliminate FlexGet’s attempts at pulling from the wrong Python version and failing.
```
$ rm /opt/bin/python
$ ln -s /opt/bin/python3 /opt/bin/python
```
Finally, we are going to upgrade pip from the outdated opkg release, and install setuptools to be able to install FlexGet.
```
$ pip3 install -–upgrade pip
$ pip install setuptools
```
## Install FlexGet

Install using the following command:
```
$ pip install flexget
```
NOTE: You will receive an error that FlexGet requires feedparser v.5.2.1, and that 6.0.0b1 is incompatible. Ignore this message as its quite the opposite since some lib2to3 requirements are either non-functional or missing in the Synology releases of Python. Without upgrading to the beta version of feedparser, you will get Syntax errors, and FlexGet will not run. You must, however install feedparser AFTER installing FlexGet, as the FlexGet installation will replace the feedparser installation.


## Verify installation
Run the following command, and FlexGet will display its version number:

```
$ flexget -V
3.1.82
You are on the latest release.
```

## Configuration
Before you can run FlexGet you must must [write a configuration file](https://flexget.com/Configuration) and test that it works correctly. FlexGet stores a number of files in the same directory as its config file so make sure the user that will be executing FlexGet can write to the appropriate path. Where you choose to place the config file is up to you. By default, FlexGet will check the following locations:
```
/volume1/homes/(username)
/usr/syno/synoman/webapi
/var/services/homes/(username)/.flexget
/var/services/homes/(username)/.config/flexget
```
You can use Config File Editor to create and write a configuration file by modifying the `Config File Editor` entry at the bottom of the dropdown list. Use the notation of `path/to/file.ext,dropdown name` to create your file. For example, if you want to use the home folder and have the dropdown list title it as `Flexget Config`, you would use:
`/volume1/homes/(username)/config.yml,FlexGet Config`

Once you have written your config file, you can check it using:
```
$ flexget check
```
If you intend to use Transmission for FlexGet to send jobs to, you can use the SynoCommunity Transmission package without issue, or you can choose to install via pip. I recommend the former, as it is easier to manage.

As with Transmission, it is not recommended to run FlexGet as the root user


## Starting FlexGet At Boot

There are several ways to boot FlexGet at startup. In this guide, I’ll go through setting up a `Task Manager` startup script, and executing it on boot.

Open `Control Panel` and navigate to `Task Manager`. Click on `Settings` and check the box to `Save output results`. Select your `Server name` from the `Select` page, and click OK. Click `Create -> Triggered Task -> User Defined Script`. `Name` the Task whatever you like, select the `User profile` who you would like to execute FlexGet, and set the `Event` to `Boot-up`. If you chose to use `Task Manager` to execute your Entware services launch, select your `Pre-task` as that script, and click `Enabled`. Navigate to Task Settings on the top bar, and in the run command type the following:
```
#!/bin/sh
exec /opt/bin/flexget daemon start -d
```
Click `OK`. Now, test your script by right clicking it in the Task Manager window and selecting `Run`. With the script still selected, go to `Action -> View Result`. If the current status is `Normal (0)`, you’re all set! If not, read the `Standard output/error` field to find out what the issue is. In most cases, it is a misplaced or incorrect config file.


# Important caveat

Be aware that with Synology, the contents of `/etc/init` and `/etc/profile` are reset to system defaults every time you install a major version OS update. So, if you choose to make any changes here (such as adding `. /opt/etc/profile` at the end of `/etc/profile` for OPKG) when you update from e.g. DSM 6.1 to DSM 6.2, your changes will get wiped out. For this reason it is important that you back them up so that you can easily replace them after updating. Minor version updates do not reset these files/folders.

## That's all, folks
The setup above will automatically start FlexGet in daemon mode whenever your Synology server boots up. Enjoy!