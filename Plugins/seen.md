= Seen =

Remembers downloaded entries across all tasks and rejects them on subsequent executions.

This plugin is enabled on all tasks by default. See plugin [wiki:Plugins/disable_builtins disable_builtins] for information how to disable builtin plugins. Note that disabling this will (likely) cause !FlexGet to download all matches on every execution!

== Local Mode ==
You may not want entries seen on some tasks to affect other tasks. Seen plugin can be put into local mode, such that it will only reject entries that have been accepted previously in the same task. You can use the following configuration to enable this mode:
{{{
seen: local
}}}

== Commanline options ==

Plugin has few command line options. See also CLI help for syntax info. (`flexget seen --help`)

=== forget ===

Option {{{seen forget <task>}}} can be used to forget everything seen from a specific task. (#301)

Option {{{seen forget <value>}}} which can be used to remove any url, title or even imdb url which already has been seen once to be downloaded again.

=== add ===

Option {{{seen add <value>}}} which can be used to add any url, title or even imdb url as already seen effectively preventing them to be downloaded.

'''Examples:'''

This is especially useful when you have downloaded something manually outside !FlexGet.

{{{
seen add "http://some.site.com/torrents/1235321"
}}}


With tasks using plugin [wiki:Plugins/seen_movies seen_movies] you can also use imdb id to mark any movie as already seen!

{{{
seen add tt0119698
}}}

'''Protip:''' In case you wish to forget manually seen stuff you can use {{{--forget "--seen"}}}

=== --learn ===
The `execute` option {{{--learn}}} (optionally combined with {{{--tasks}}}) can be used to mark all entries that would be accepted as seen.