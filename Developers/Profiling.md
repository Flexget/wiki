---
title: Profiling
description: 
published: true
date: 2022-09-18T04:57:20.085Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:17.551Z
---

# How to profile FlexGet
Quick hack:

With dev sanbdox, copy `bin/flexget` to `bin/profile` and modify it a bit ..

```
__requires__ = 'FlexGet==1.0-svn'
import sys
from pkg_resources import load_entry_point

import profile


profile.run("""
sys.exit(
   load_entry_point('FlexGet==1.0-svn', 'console_scripts', 'flexget')()
)""")
```

And run it like

```
bin/profile > profile.txt
```