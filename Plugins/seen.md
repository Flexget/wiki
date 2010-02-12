= Seen =

Remembers downloaded entries across all feeds and rejects them on subsequent executions.

This plugin is enabled on all feeds by default. See plugin [wiki:Plugins/disable_builtins disable_builtins] for information how to disable builtin plugins. Note that disabling this will (likely) cause !FlexGet to download all matches on every execution!

== Commanline options ==

Plugin has few command line options starting from bleeding edge / 1.0

=== --forget ===

Option {{{--forget <feed>}}} can be used to forget everything seen from a specific feed. (#301)

=== --seen ===

Option {{{--seen <value>}}} which can be used to add any url, title or even imdb url as already seen effectively preventing them to be downloaded.

'''Examples:'''

This is especially useful when you have downloaded something manually outside !FlexGet.

{{{
--seen "http://some.site.com/torrents/1235321"
}}}


With feeds using plugin [wiki:Plugins/seen_movies seen_movies] you can also use imdb url to mark any movie as already seen!

{{{
--seen "http://www.imdb.com/title/tt0119698/"
}}}

'''Protip:''' In case you wish to forget manually seen stuff you can use {{{--forget "--seen"}}}