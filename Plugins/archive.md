== Archive ==

The archive plugin will keep a history of all entries from a given task, whether they have been accepted or not. This archive can then later be searched, and entries injected into a task again.


Simply enable without any tagging.

{{{
archive: yes
}}}

With tagging:

{{{
archive: [torrent, tv]
}}}

Search:

{{{
archive search [@TAG] [@TAG] KEYWORD
}}}

Note: if keyword has spaces it must be quoted.

Retrieve (inject into task):

{{{
archive inject ID [FORCE]
}}}

== Urlrewriter ==

{{{
flexget_archive: yes
}}}

or

{{{
flexget_archive: [tag, tag]
}}}

This works with [wiki:Plugins/discover discover] and also with urlrewriting but has less use in there.