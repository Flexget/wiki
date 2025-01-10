---
title: uv install
description: Installing FlexGet using uv
published: true
date: 2025-01-10T03:31:25.007Z
tags: 
editor: markdown
dateCreated: 2025-01-10T03:22:17.273Z
---

# Installing FlexGet with uv
[uv](https://docs.astral.sh/uv/) is a multi-faceted tool with many purposes, but one of them ([uv tool](https://docs.astral.sh/uv/guides/tools/)) is to easily install python based CLI tools (like FlexGet!) and not worry about the virtual environment or python management yourself. Here are the steps to install and update FlexGet using uv tool.

### Install uv
Instructions can be found [at the uv website.](https://docs.astral.sh/uv/getting-started/installation/)

### Install FlexGet
We can then use uv to install FlexGet.
```
uv tool install flexget[locked]
```
This will install FlexGet into a uv managed virtual environment, and add the binaries to your PATH. The `locked` extra is not required, but is recommended, and makes sure you get the exact dependencies that we are testing with in our CI.

#### Specifying python version
You can also specify what version of python you would like to use
```
uv tool install flexget[locked] --python 3.12
```

#### Adding extra dependencies
If you need extra dependencies in your environment, they can also be specified.
```
uv tool install flexget[locked] --with transmission-rpc
```

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
if you need to get a specific version, you can specify it
```
uv tool upgrade flexget==3.13.10
```

## Next Step

Choose your OS to continue setting up scheduling:
 * [Linux](/InstallWizard/Linux/Scheduling)
 * [Windows](/InstallWizard/Windows/Scheduling)
 * [Mac OSX](/InstallWizard/OSX/Autorun)