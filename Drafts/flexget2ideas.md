---
title: flexget2ideas
description: 
published: true
date: 2022-09-18T04:58:44.192Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:41.541Z
---

# Ideas for larger changes that may come with flexget 2
All input on any of these ideas is welcome.

### Plugins
Problem: Right now, we have one mount point for plugins, and keep track of which interface they use by the 'groups' attribute of the plugin. Some plugins don't even register to that mount point (scheduler, api_tvdb) and work totally based on hooks or explicit calls.

Better ways?: http://martyalchin.com/2008/jan/10/simple-plugin-framework/ This describes a very simple framework where it is easy to register and keep track of plugins at various mount points. It would also make it very easy for a plugin itself to define a new mount point for plugins. Mountpoints I would imagine having in this system: processor plugins (the ones that go in tasks), thread plugins (like scheduler), search plugins, urlrewrite plugins, (and probably more.) The class for each of these would be an easy place to document what the interface for interacting with each of these types of plugins was (whereas right now there is no clear place to document interfaces for things like search or urlrewrite plugins.)

### Pipelines
- Would be nice to ditch phases and priorities entirely, and lay out tasks like yahoo pipes, with forking and merging allowed. Plugins that currently hook multiple phases mostly do so to record whether an entry made it all the way to output in their database, this can be replaced with events on the entries that plugins can hook.

  Problem: replacing builtins. Will have to look closer at how these are used, haven't started planning this yet.

- Problem: Attempt to standardize the free for all we currently have with entry fields.

  Solution?: Ditch unmanaged entry fields. Entries will have one required attribute, which is title. We will then have a set of predefined tags which can be applied to entries. A tag may also contain a set of required (and/or optional) fields that come with it. The list of defined tags should be easily extended by a plugin. Then processing plugins would declare tags that an entry requires in order to be processed by that plugin. Example: The 'episode' tag would have 'series' and 'identifier' as required fields (i.e. any entry tagged as an episode is guaranteed to have that info) Some plugin like exists_series would then declare that an entry requires the 'episode' tag in order to be processed. If plugins also declared what tags they add during processing, this means we could report all these tag errors before even attempting to run a task (in a config validator or editor.) example snippet:
```
if 'episode' in entry.tags:
  if entry.episode.identifier in my_database:  # Maybe access tag fields under a tag namespace like this?
    # do something
```

What a config editor might look like: (Panel on the left would be different plugins. Clicking on a plugin would allow changing configuration, which might change what input and output nodes it has.)

<img src="http://i.imgur.com/gLPVgbk.png">