---
title: digest
description: 
published: true
date: 2022-09-18T05:03:44.882Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:03:42.246Z
---

# Digest
This plugin works as an output plugin, and collects entries from tasks to be combined into another task (usually for notification.) The `from_digest` plugin is then used in the task where the entries should be acted upon, e.g. notifications sent.

## Configuration
```text
digest: <listname>
```
or
```text
digest:
  list: <listname>
  state: [accepted|rejected|failed|undecided]
```
You can also specify a list of states to be digested.
```text
digest:
  list: <listname>
  state:
    - accepted
    - failed
```

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