---
title: InstallVirtualenv
description: 
published: true
date: 2022-09-18T05:24:02.426Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:23:59.824Z
---

### Install FlexGet in the virtualenv
```
cd ~/flexget
bin/pip install flexget
```

(If your virtualenv does not include pip, run `bin/easy_install pip` first.)

This will install FlexGet and all the required dependencies.

### Running FlexGet from the virtualenv
You can either activate the virtualenv with the command:

```
source ~/flexget/bin/activate
```

After that command `flexget` works from anywhere. Or you can run it via:

```
~/flexget/bin/flexget [options](/options)
```

Also use remember to use this explicit path for any crontab, daemon, or other cli executions!
