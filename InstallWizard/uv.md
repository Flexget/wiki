---
title: Install FlexGet with uv
description: Installing FlexGet using uv
published: true
date: 2025-04-23T08:17:24.332Z
tags: 
editor: markdown
dateCreated: 2025-01-10T03:22:17.273Z
---

# Installing FlexGet with uv
[uv](https://docs.astral.sh/uv/) has multiple purposes, but one of them ([uv tool](https://docs.astral.sh/uv/guides/tools/)) is to easily install python based CLI tools (like FlexGet!) and not worry about the virtual environment or python management yourself. Here are the steps to install and update FlexGet using uv tool.

### Install uv
Instructions can be found [at the uv website.](https://docs.astral.sh/uv/getting-started/installation/)

### Install FlexGet
We can then use uv to install FlexGet:
```
uv tool install flexget
```
or with fully locked dependency versions:
```
uv tool install flexget[locked]
```
This will install FlexGet into a uv managed virtual environment, and add the binaries to your PATH.

The `locked` extra is not required, but is recommended, because it makes sure you get the exact dependencies that we have tested with.

#### Specifying python version
You can also specify what version of python you would like to use
```
uv tool install flexget[locked] --python 3.13
```

#### Adding extras
There are several extras we include that install optional dependencies needed by some of the most common plugins. They are:
- [deluge](/Plugins/deluge)
- [qbittorrent](/Plugins/qbittorrent)
- [transmission](/Plugins/transmission)
- [telegram](/Plugins/Notifiers/telegram)
- all (this will include all 4 of the above)

You can specify them when installing and an appropriate version of the dependency will be installed and upgraded alongside flexget for you. e.g.
```
uv tool install flexget[locked,all]
uv tool install flexget[locked,deluge,telegram]
```

If you need extra dependencies other than the extras listed above, they can also be specified.
```
uv tool install flexget[locked] --with myotherdependency
```
> If you later decide you want to switch python versions or change extras, you can simply run the `uv tool install` command again with your new options.
{.is-info}

### Run FlexGet
FlexGet will be added to your PATH, so you can run it from anywhere.
```
flexget --help
```

### Updating
To update to the latest version of FlexGet, you can run:
```
uv tool upgrade flexget
```
If you need to get a specific version, you can specify it:
```
uv tool upgrade flexget==3.15.36
```
> You probably don't want to specify a specific FlexGet version during `uv tool install`, as this version constraint will keep applying when you try to `uv tool upgrade` later. It is better to do the install, then "upgrade" to the specific version you need right now.
{.is-warning}

### Uninstalling
If you installed with this method, you can:
```
uv tool uninstall flexget
```

## Next Step

Choose your OS to continue setting up scheduling:
 * [Linux](/InstallWizard/Linux/Scheduling)
 * [Windows](/InstallWizard/Windows/Scheduling)
 * [Mac OSX](/InstallWizard/OSX/Autorun)