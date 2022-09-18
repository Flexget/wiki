---
title: Plugbox
description: 
published: true
date: 2022-09-18T05:00:26.122Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:23.622Z
---

## Plugbox
Wiki explaining installation [here](http://plugapps.com/index.php5?title=Application:Flexget).

However it seems to discourage upgrading to Python 3 in PlugBox. This shouldn't be a problem since you can install 2.x alongside 3.x just fine.

According to post [here](http://plugboxlinux.org/forum/viewtopic.php?f=9&t=368&start=10#p3071) the following should work fine if you are running Python 3.

```
pacman -S python2 python-distribute
easy_install-2.7 pip
pip install flexget
```

**Note:** There will be some GCC compiler complaints about optional speedups. Ignore these, those will fall back to pure python.

To verify installation:

```
flexget -V
```