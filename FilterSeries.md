= Series =

Intelligent filter for tv-series. This solves duplicate downloads
problem that occurs when using patterns (regexp) matching since same
episode is often released by multiple groups.

'''Example configuration:'''

{{{
series:
  - some serie
  - another serie
}}}

If {{{some serie}}} and {{{another serie}}} have understandable episode
numbering any given episode is downloaded only once.

So if we get same episode twice:

Some.Series.S2E10.More.Text[[BR]]
Some.Series.S2E10.Something.Else

Only one of them is downloaded, which one depends on various options.

If two different qualities come available at the same moment,
!FlexGet will always download the better one.

== Timeframe ==

Series filter allows you to specify a timeframe for each series in which
flexget waits better quality.

'''Example configuration:'''

{{{
series:
  - some serie:
      timeframe:
        hours: 4
        enough: 720p
  - another series
  - third series
}}}

In this example when a epsisode of {{{some serie}}} appears, !FlexGet waits 4 hours for other versions to appear and then proceeds to download best one available.

The enough parameter will specify quality that you find good enough to start
downloading without waiting whole timeframe. If qualities meeting enough parameter
and above are available, !FlexGet will prefer the enough. Ie. if enough value is set
to 'hdtv' and qualities dsr, hdtv and 720p are available, hdtv will be chosen.
If we take hdtv off from list, 720p would be downloaded.

Enough has default value of 720p.

Possible values for enough (in order): 1080p, 1080, 720p, 720, hr, dvd, hdtv, dsr, dsrip

== Custom path ==

Specify download path for series.

Example:

{{{
series:
  - some series:
      path: ~/download/some_series/
  - another series
  - third series
}}}

Example with timeframe:

{{{
series:
  - some series:
      timeframe:
        hours: 4
      path: ~/download/some_series/
  - another series
  - third series
}}}

== Advanced matching with regexps ==

The standard name matching is not perfect, if you're used to working with regexps you can
specify regexp(s) that are used to test if entry is episode of given serie.

You can also give regexps for episode number matching and unique id matching.

Example:

{{{
series:
  - some serie:
      name_patterns: ^some.serie
      ep_patterns: (\d\d)-(\d\d\d)  # must return TWO groups
      id_patterns: (\d\d\d)         # can return any number of groups
}}}

All above patterns also accept multiple regular expressions.

{{{
name_patterns:
  - ^some.series
  - ^some
}}}

== Define default settings for all series ==

''TODO: document better''

To change serie default settings you can use [wiki:SettingsSection settings section] block which is similar to ([wiki:GlobalSection] global section). This must be in configuration "root level". Validation does not apply to here, and this section may be changed at some point ... 

{{{
settings:
  series:
    timeframe:
      hours: 3
      quality: 720p
}}}