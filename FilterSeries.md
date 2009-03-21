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
numbering any given episode is downloaded only once. !FlexGet should support all known episode numbering schemes without any configuration, including dates.

So if we get same episode twice:

Some.Series.S2E10.More.Text[[BR]]
Some.Series.S2E10.Something.Else

Only one of them is downloaded, which one depends on various options.

'''Notes:'''

 * If you wish to get just certain qualities, currently best way to do this is described in [wiki:CookBook#Series-getonlycertainqualities cook book]. Easier and more customizable approaches are being worked on.
 * If multiple different qualities come available at the same moment, !FlexGet will always download the best one.
 * Ideally configured series name should not contain anything else than a series name. This is because if you change or reformat name !FlexGet will lose track of already downloaded episodes.

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
If we take hdtv off from list, 720p would be downloaded. Note that the enough value does '''not''' guarantee that the downloaded episode is what has been specified. It can be higher and lower. This is somewhat confusing to use and will be made more user friendly in 1.0 release.

Enough has default value of 720p. If you're only interested in 720p quality you can take advantage of this and leave enough out completely.

'''Example:''

{{{
series:
  - first series: { timeframe: { hours: 48 } }
  - another series: { timeframe: { hours: 16 } }
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
specify regexp(s) that filter for the show's name, episode number or unique identifier.

'''Note:''' Use this only if you're having problems with matching, it should be able to handle 99% of cases without any regexp tweaking.

=== Example ===

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


ep_patterns are useful for shows enumerated by season and episode numbers (eg, S04E01).  The default episode regular expressions used are
{{{
ep_patterns:
  - s(\d+)e(\d+)
  - s(\d+)ep(\d+)
  - (\d+)x(\d+)
}}}
The two groups returned by the episode regular expression should be numbers.

id_patterns are useful for series with shows that are not enumerated by season/episode numbering.  The default id_patterns regexps are useful for dated episodes.  They are set as
{{{
id_patterns:
  - (\d\d\d\d).(\d+).(\d+)
  - (\d+).(\d+).(\d\d\d\d)
  - (\d\d\d\d)x(\d+)\.(\d+)
}}}

User defined episode or id matching takes priority over the built-in expressions.



== Watched ==

Some feeds may occasionally contain older episodes that have already been watched by user but not seen be !FlexGet. For these you can define watched.

{{{
series:
  - some series:
      watched:
        season: 3
        episode: 3
}}}

This is however quite inconvenient. In future !FlexGet will not download older episodes than what user is "currently watching" automaticly (Ticket #92).

== Define default settings for all series ==

[wiki:ToBeRemoved TO BE REMOVED]. Will be replaces with better alternative because of some [wiki:SettingsBlockProblems problems].

But for 0.9 this is still valid and easy way to customize timeframe globally.

To change a series default settings you can use [wiki:SettingsSection settings section] which is similar to ([wiki:GlobalSection] global section). This must be in configuration "root level". This removes need to specify desired base-line settings for each series. Validation does not apply to here, and this section may be changed at some point ...

{{{
settings:
  series:
    timeframe:
      hours: 3
      enough: 720p
}}}

