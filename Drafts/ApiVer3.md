---
title: ApiVer3
description: 
published: true
date: 2022-09-18T04:57:27.648Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:25.052Z
---

# Some sketches for api_ver 3
We're planning to move away from task.entries and instead pass iterable to the plugin, new method signature will be:

```
def on_task_xxx(self, task, config, entries):
```

## Iterating entries
This is still the open question.

### Option 1 - helpers
```
from flexget.entry import accepted, rejected, undecided

# and then iterating
for entry in accepted(entries):
  pass

for entry in accepted(undecided(entries)):
  pass
```

* Old task.entries contained undecided AND accepted, iterating them like this feels messy
* Requires imports

### Option 2 - generator expression
```
for entry in (e.accepted for e in entries):
  e.reject()
```

* Slightly more verbose
* Feels very pythonic and is very explicit
* Iterating the old task.entries is even more verbose - and we do this most

```
for entry in (e.accepted or e.undecided for e in entries):
  e.reject()
```

This could be alleviated with new property, but it might just make things more confusing, explicit is better than implicit .. right?

```
for entry in (e.active for e in entries):
  e.reject()
```

### Option 3 - properties
If/since our entries is custom list class, we could use properties from it.

```
for entry in entries.accepted:
  entry.reject()
```

* Similar problem, how to loop through old task.entries
* I'm not aware of any other python iterable that has built in filtering methods

