---
title: from_digest
description: 
published: true
date: 2022-09-18T05:05:35.303Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:05:32.750Z
---

# From Digest
This plugin outputs entries which have been collected by the [digest](/Plugins/digest) plugin. See [that](/Plugins/digest) wiki page for more usage examples.


## Configuration
```text
from_digest: <listname>
```
or
```text
from_digest:
  list: <listname>
```
You can also `limit` the number of entries to output, as well as manage how long before they `expire` (i.e. removed from the list) as follows:
```text
from_digest:
  list: <listname>
  limit: <number of items>
  expire: <time to expire> 
```
Once an entry has been outputted it will be removed from the digest by default, you can stop this behaviour by setting `expire: no`.

## Examples
These examples are incomplete, and contain comments where other plugins should be set up.
### Daily Email
```yaml
tasks:
  download task 1:
    # some stuff to do downloads
    digest:
      list: daily email
      state:
        - accepted
        - failed

  download task 2:
    # some stuff to do downloads
    digest: daily email

  daily email task:
    from_digest:
      list: daily email
      restore_state: yes
    seen: no
    email:
      # the email settings

schedules:
- tasks: [download task 1, download task 2]
  interval:
    hours: 1
- tasks: daily email task
  interval:
    days: 1
```

### Last 50 entries HTML
```yaml
tasks:
  download task 1:
    # some stuff to do downloads
    digest: recently accepted

  download task 2:
    # some stuff to do downloads
    digest: recently accepted

  generate html:
    from_digest:
      list: recently accepted
      limit: 50
      expire: no
    accept_all: yes
    seen: no
    make_html:
      # the make_html settings

schedules:
- tasks: [download task 1, download task 2, generate html]
  interval:
    hours: 1
```