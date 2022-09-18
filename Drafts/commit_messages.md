---
title: commit_messages
description: 
published: true
date: 2022-09-18T04:58:36.520Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:33.857Z
---

# New Changelog Generator
A proof of concept implementation and example output is here: https://gist.github.com/gazpachoking/2f9c9ba49baede94b3f6

Make a new markdown based changelog generator, which will eventually automatically commit to wiki git repo (when we implement that.) The changelog can also be manually fixed/edited/updated from the wiki. The generator would add messages from all commits which start with a valid bracket tag. Include comments in the changelog, which the generator uses to insert new content. It stores the last processed git commit in one of these comments to know where to continue from when run again. New tagged commits will be sorted into their section in between the comments (sections created if needed.) When generator finds a tagged release, it moves the contents between the comments below the end comment, then adds a tag for the release number. Example:

```
# FlexGet Change Log
<-- begin:aab4b4ab4this_is_the_last_git_hash_processed -->
## Version 1.2.3235 (Unreleased)
### Features
* blah
### Bug Fixes
* blah blah
<-- end -->
## Version 1.2.3234 (2016-2-20)
...
```


## Bracket Tags
Start each commit with one or more tags in brackets, to split changelog into categories.

category tags: (these should sort into sections)
* fix: fixes a bug
* add: new feature added
* change: change in existing functionality
* remove
* deprecate
optional tags: (these would remain in the commit message, just to clarify them)
* plugin_name: use the plugin name if message is ambiguous
special tag:
* action: This means a config upgrade action is needed. The generator should add a stub to the upgrade actions wiki page, and a link from the changelog item. The wiki pages can then be manually augmented as needed.

## Ticket References
Ticket references should be at the end of the commit message, references are to github issue numbers. `fix #123` (to close ticket when merged), `ref #123` (to put a message in ticket) Changelog generator should turn these into markdown links.

## Examples
* `[fix](/fix) Rss plugin doesn't crash with invalid urls. fix #123`
* `[fix](/fix) [pushover](/pushover) Always sets defaults for all fields. fix #123`
* `Move dependency requirement comments inline with dependencies.`