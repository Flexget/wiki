= Command Line --feed option =

Allows running only selected feeds from the config.

'''Syntax:'''

{{{        
--feed <FEED>[,FEED]
}}}

where the given feed names can also be glob patterns (i.e. using `*`, `?` or `[charsets]`).


'''Example:'''

If you want to only execute a feed called {{{myfeed}}} run flexget like so:
{{{
flexget --feed myfeed
}}}

'''Multiple feeds example:'''

If you would like to run multiple feeds you can list them with comma separators (and no space.) This example runs {{{myfeed}}} and {{{yourfeed}}}:
{{{
flexget --feed myfeed,yourfeed
}}}

'''Pattern example:'''

If you would like to select a number of feeds that have similar names:
{{{
flexget --feed "tv*"
}}}


'''Grouping feeds by poll frequency:'''

Another very useful application of the pattern selection is to have cron schedules like this:
{{{
*/5     * * * *         nice flexget --cron --feed "*-5"
*/14    * * * *         nice flexget --cron --feed "*-14"
}}}

You just need to append one of the supported poll intervals to your feed names, and they'll get  automatically polled with that frequency. Note that the schedules are never triggered at the same minute, so they can never directly collide (if you have very slow feeds, some executions ''might'' be skipped due to the lock of a still running process).
