---
title: Developers
description: 
published: true
date: 2026-01-09T15:39:06.655Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:49:11.127Z
---

# Documentation
View the documentation and tutorials at [flexget.readthedocs.org](https://flexget.readthedocs.org/en/latest/)

## Contributing
Making custom plugins should be easy for anyone with some python experience.

If you're working on good re-usable plugin we're be more than happy to include it in official distribution. See [Contribute](/Contribute) for more information.

## Unit testing
FlexGet has over 1200 unit tests so chances are that if your modifications pass the tests nothing major has been broken.

## Enhancement proposals
 * [Roadmap](/Roadmap)

## Running IPython inside FlexGet
First install IPython

```bash
bin/pip install ipython
```

And then place this where you wish to hack:

```
import IPython; IPython.embed()
```

### Attachments  

* [events in feed](/attachments/Developers/flexget_events.png)
