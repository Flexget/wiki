= Command Line --feed option =

Allows running only selected feeds from the config.

'''Syntax:'''

{{{        
--feed <FEED>[,FEED]
}}}

'''Example use:'''

If you want to only execute a feed called {{{myfeed}}} run flexget like so:
{{{
flexget --feed myfeed
}}}

'''Example use 2:'''

If you would like to run multiple feeds you can list them with comma separators (and no space.) This example runs {{{myfeed}}} and {{{yourfeed}}}:
{{{
flexget --feed myfeed,yourfeed
}}}