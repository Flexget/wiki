---
title: FlexgetV3
description: 
published: true
date: 2022-09-18T04:57:58.016Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:55.413Z
---

# Flexget V3 - Drop Py2 support

Python 2 EOL is 2020-01-01 which means now is a good time for us to start dropping it completely.

## Prepearations 

- Stabalize/add Online tests

## Checklist:

- Research which dependencies we currently use that are py2 only
- Drop `__future__` usage
- Drop `future` and its realted libs usage
- Drop `six`
- Drop `builtins` 
- Drop `path.py` and `pathlib` for stdlib `pathlib`

### Lower priority:

- Remove all inheritence from `object` from all classess
- 


### Py2 only deps that we'll drop/update and plugins that use them

- deluge/deluge [Done](https://github.com/Flexget/Flexget/pull/2102)
- mechanize/form [Done](https://github.com/Flexget/Flexget/pull/2224)

## Open questions?

- Should we support "maintenance" stuff for flexget 2.x? Is it that even feasible with our current infrastructure?
- Is there any thing else we wanna change with this version? Maybe replace argparse with click?

### Nice to have changes

- Replace `argparse` with `click`?
- Use `pendulum` or `arrow` for all our date/datetime/timedelta/timezone needs?
- Replace `beautifulsoup` with `requests-html`?
- `apscheduler` is giving us a hard time. Should it be replaced?
