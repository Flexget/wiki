= Series =

Intelligent filter for tv-series. This solves duplicate downloads
problem that occurs when using patterns (regexp) matching since same
episode is often released by multiple groups.

'''Simple configuration:'''

{{{
series:
  - some series
  - another series
}}}

If {{{some series}}} and {{{another series}}} have understandable episode
numbering any given episode is downloaded only once.

So if we get same episode twice:

Some.Series.S2E10.More.Text[[BR]]
Some.Series.S2E10.Something.Else

Only one of them is downloaded, which one depends on various options.

If multiple different qualities come available at the same moment, !FlexGet will always download the best one.

Ideally configured series name should not contain anything else than a name. This is because if you change or reformat name !FlexGet will lose track of already downloaded episodes.

== Timeframe ==

Series filter allows you to specify a timeframe for each series in which
!FlexGet waits better quality.

'''Example configuration:'''

{{{
series:
  - some series:
      timeframe:
        hours: 4
        enough: 720p
  - another series
  - third series
}}}

In this example when a epsisode of {{{some series}}} appears, !FlexGet waits 4 hours for other versions to appear and then proceeds to download best one available.

The enough parameter will specify quality that you find good enough to start
downloading without waiting whole timeframe. If qualities meeting enough parameter
and above are available, !FlexGet will prefer the enough. Ie. if enough value is set
to 'hdtv' and qualities dsr, hdtv and 720p are available, hdtv will be chosen.
If we take hdtv off from list, 720p would be downloaded.

Enough has default value of 720p. If you're only interested in 720p quality you can take advantage of this.

'''Example:''

{{{
series:
  - first series: { timeframe: 48 }
  - another series: { timeframe: 16 }
  - third series
}}}

'''Note:''' This is written in yaml in-line form to make it more compact. 

Possible values for enough (in order): 1080p, 1080, 720p, 720, hr, dvd, hdtv, dsr, dsrip

== Override path ==

Specify a custom path for a series. Note that this does '''not''' download it, your feed must use [wiki:OutputDownload download] module to do that.

'''Example:'''

{{{
series:
  - some series:
      path: ~/download/some_series/
  - another series
  - third series
download: ~/download/
}}}

Series {{{another series, third series}}} will be downloaded into {{{~/downloads}}}. However {{{some series}}} has overriden path and will be downloaded into {{{~/downloads/some_series/}}}.

'''Example with timeframe:'''

{{{
series:
  - some series:
      timeframe:
        hours: 4
      path: ~/download/some_series/
  - another series
  - third series
download: ~/download/
}}}

== Advanced matching with regexps ==

The standard name matching is not perfect, if you're used to working with regexps you can
specify regexp(s) that are used to test if entry is episode of given serie.

You can also give regexps for episode number matching and unique id matching.

Example:

{{{
series:
  - some series:
      name_patterns: ^some.series
      ep_patterns: (\d\d)-(\d\d\d)  # must return TWO groups
      id_patterns: (\d\d\d)         # can return any number of groups
  - another series
  - third series
}}}

All above patterns also accept multiple regular expressions.

{{{
name_patterns:
  - ^some.series
  - ^something.entirely.different
}}}

== Define default settings for all series ==

''TODO: document better''

To change a series default settings you can use [wiki:SettingsSection settings section] which is similar to ([wiki:GlobalSection] global section). This must be in configuration "root level". This removes need to specify desired base-line settings for each series. Validation does not apply to here, and this section may be changed at some point ...

{{{
settings:
  series:
    timeframe:
      hours: 3
      quality: 720p
}}}