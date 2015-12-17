= Standardized commit messages =

Idea would be to tag commits consistently, so that we can improve our changelog generator to be a little more user friendly.

Changelog generator will show all commits directly to master, and merge commits when other branches (PRs) are merged in.
This means all commits directly to master should follow this format, and when merging PRs, the message should be changed to comply when merging (this becomes the second line of the merge commit message.)
Any feature branches should be merged into develop (not the other way around) and should not allow a fast forward, in order that we can make format the message for the merge commit properly. If this sounds like git magic, submitting a pr is an easier way, as it will ensure the merge goes the right direction, and gives you a chance to edit the merge commit message before merging.

== Bracket Tags ==

Start each commit with one or more tags in brackets, to split changelog into categories.

tag ideas:
* fix: fixes a bug
* feature: new feature added


== Ticket References ==
Ticket references should be at the end of the commit message

== Examples ==

* `[fix] Rss plugin doesn't crash with invalid urls. fix #123`