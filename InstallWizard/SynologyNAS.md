---
title: SynologyNAS
description: 
published: true
date: 2022-11-22T17:36:09.372Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:35.039Z
---

# [Install Wizard](/InstallWizard) > SynologyNAS

There are a few different ways to go about running FlexGet on your NAS. They are listed below in order of preference.

## [Docker container](/InstallWizard/SynologyNAS/Docker)

Running FlexGet in a Docker container gives you the ultimate level of control over its environment.

## [Local Python package](/InstallWizard/SynologyNAS/PythonPackage)

> FlexGet supports Python 3.7 and later
{.is-warning}

This method uses the Python installation available from Entware-ng's opkg Package Center. This is a relatively easy process for anyone with basic CLI experience, but does require some maintenance and troubleshooting.

## Synocommunity package

The [synocommunity](https://synocommunity.com/) repository includes a FlexGet package for DSM.

If you are less comfortable with the command line, you may find this method easier. It will be, however, be more difficult to maintain, and has the least amount of documentation to help with errors. You must also wait for the package maintainers to update the FlexGet package; with the above methods, updates to FlexGet may be installed as soon as they are released.

Follow the homepage instructions to add synocommunity to your NAS, and then install Python and FlexGet through the web interface. The config file is located at `/usr/local/flexget/var/config.yml` on DSM v6 and at `/var/packages/flexget/target/share/config.yml` on DSM v7 RC.
