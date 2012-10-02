= Inject =

Allows injecting imaginary entry for !FlexGet to process.

'''Syntax:'''

{{{        
--inject <TITLE> [URL] [ACCEPT] [FORCE]
}}}
        
Without URL a random url will be generated. All other inputs are disabled.

'''Example use:'''
        
{{{
flexget --inject "Some.Series.S02E12.Imaginary" --task my-series --learn
}}}
        
This would inject imaginary series into a single task and learn it as a downloaded,
assuming task accepts the injected entry.

'''Example use 2:'''
        
{{{
flexget --task=some.task --inject "Some.Title" "Some.direct.url" yes yes
}}}
        
This would inject imaginary title with direct link to file into a single task, accept it and force it trough even if some filter tries to reject it.

=== Setting Entry Fields ===
You can also set arbitrary [wiki:Entry entry fields] when injecting. This is done in entryfield=value format. These can be listed at any point after the url.

'''Example:'''

{{{
flexget --task=some.task --inject "Some Title" "Some.direct.url" no no imdb_id=tt33333
}}}