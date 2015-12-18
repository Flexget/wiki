= Standardized commit messages =

Idea would be to tag commits consistently, so that we can improve our changelog generator to be a little more user friendly.

Changelog generator will show all commits directly to develop, and merge commits when other branches (PRs) are merged in.[[BR]]
This means all commits directly to develop should follow this format, and when merging PRs, the message should be changed to comply when merging (this becomes the second line of the merge commit message.)[[BR]]
Any feature branches should be merged into develop (not the other way around) and should not allow a fast forward, in order that we can make format the message for the merge commit properly.[[BR]]
If this sounds like git magic, submitting a pr is an easier way, as it will ensure the merge goes the right direction, and gives you a chance to edit the merge commit message before merging.[[BR]]


== Bracket Tags ==

Start each commit with one or more tags in brackets, to split changelog into categories.

tag ideas:
* fix: fixes a bug
* feature: new feature added
* refactor: core code changes and/or updates
* plugin_name: use the plugin name if message is ambiguous
* dev: hide commit from user changelog (use as first tag)?


== Ticket References ==
Ticket references should be at the end of the commit message, references are to github issue numbers. `fix #123` (to close ticket when merged), `ref #123` (to put a message in ticket)

== Examples ==

* `[fix] Rss plugin doesn't crash with invalid urls. fix #123`
* `[fix] [pushover] Always sets defaults for all fields. fix #123`
* `[dev] [refactor] Move dependency requirement comments inline with dependencies.`