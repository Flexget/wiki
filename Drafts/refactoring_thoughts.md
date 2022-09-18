---
title: refactoring_thoughts
description: 
published: true
date: 2022-09-18T04:59:03.333Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:59:00.694Z
---

Just brainstorming on things that can be looked at if we attempt a major refactor.

Things to handle better:
- cli plugins: There is no need to run an execution for many of our cli plugins. It would be nice if they could register to handle those cli flags without registering to the task interface. examples: --series, --movie-queue, --history. It would also be nice to release the database lock requirement for these. If we move to a daemon model, can we make it so that we can pass these requests to the running daemon separate from the execution queue.
- sub plugins:
  - It would be nice if certain plugins could enable other plugins in some way on a subset of entries. e.g. series plugin run subplugins for only particular series. regexp plugin run subplugins for particular matches.
  - Where we currently allow input plugins as sub-plugins, it would be nice if we could also allow other plugins in the chain. e.g. the ability to manipulate or filter directory names before being fed to import_series.
- plugins on multiple phases: This relates to sub-plugins, in that it makes them difficult.
  - issue: series plugin cannot run content_size type plugin as a sub-plugin since content_size needs to wait until modify phase to do its work. 
  - reruns. Due to the nature of our phases, when plugins like content_size reject, we need to rerun the entire feed to see if a different plugin would have picked something different.
- process_start, end: I don't really like these phases.
  - Most plugins that run on process start and end do not need to run on each task that they are enabled on, just once at the process start. Some of this can be solved if we handle cli plugins better, see above. Also, process_start and end are somewhat confusing if we move to a daemon model. Are they really at process start, or at execution start?
  - make_rss uses process_end to summarize information from the different tasks that ran during an execution. This should really be an execution_end phase, but it would be nice if summary plugins should not be just restricted to running after an 'execution'. This will become especially apparent if we allow a daemon mode when tasks are running on different schedules.
- plugin dependencies: Some plugins require dependencies that do not come with the project. e.g. deluge, transmission. It would be nice to have some way to cause errors, only when they are explicitly enabled by the user, other than to check in process_start and abort the feed.

ideas:
- single process method per plugin:
  - good:
    - calling subplugins is much easier
  - problems:
    - how do we deal with plugins that need to run at later times, e.g. content_size. We could have them register for later entry events, rather than task phases. content_size could register for changes to content_size field. It could register for some other entry phase, such as before_output, to enforce strict mode.
- plugins process a single entry at a time:
  - good:
    - dynamic flow between plugins would be better, entries do not all have to follow the same path.
  - problems:
    - plugins that choose based on all the possibilities. series plugin chooses the best quality among all available that fulfils quality requirement. episode advancement could be an issue if many episodes come at once out of order if series plugin cannot see them all at once.
- plugins can be registered to receive a custom list of entries to process. This is how I am implementing things in new_timeframe branch.
  - good:
    - easy for plugins to register subplugins on a subset of entries from a task, even if subplugin must run on a later phase