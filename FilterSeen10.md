= Seen =

Remembers downloaded entries across all feeds and rejects them on subsequent executions.

This plugin is enabled on all feeds by default. See plugin [wiki:ModuleDisableBuiltins disable_builtins] for information how to disable builtin plugins. Note that disabling this will cause !FlexGet to download all matches on every execution!

== Commandline option ==

Plugin adds option {{{--seen <value>}}} which can be used to add any url, title or even imdb url as already seen effectively preventing them to be downloaded.

'''Examples:'''

This is especially useful when you have downloaded something manually outside !FlexGet.

{{{
--seen "http://some.site.com/torrents/1235321"
}}}


With feeds using plugin [wiki:FilterSeenMovies seen_movies] you can also use imdb url to mark any movie as already seen!

{{{
--seen "http://www.imdb.com/title/tt0119698/"
}}}