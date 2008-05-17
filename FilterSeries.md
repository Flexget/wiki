= Series =

== Not yet stable! If using, update often! ==

Intelligent filter for tv-series. This solves duplicate downloads
problem that occurs when using patterns (regexp) matching since same
episode is often released by multiple groups.

'''Example configuration:'''

{{{
series:
  - some series
  - another series
}}}

If "some series" and "another series" have understandable episode
numbering any given episode is downloaded only once.

So if we get same episode twice:

Some.Series.S2E10.More.Text[[BR]]
Some.Series.S2E10.Something.Else

Only first file is downloaded.

If two different qualities come available at the same moment,
flexget will always download the better one. (more options coming ..)


== Advanced usage with regexps ==

The standard name matching is not perfect, if you're used to working with regexps you can
specify regexp that is used to test if entry is serie.

You can also give regexps to episode number matching and unique id matching.

Example:

{{{
series:
  - some serie:
      name_patterns: ^some.serie
      ep_patterns: (\d\d)-(\d\d\d)  # must return TWO groups
      id_patterns: (\d\d\d)         # can return any number of groups
}}}

== Timeframe ==

Series filter allows you to specify a timeframe for each series in which
flexget waits better quality.

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

In this example when a epsisode of 'some series' appears, flexget waits 4 hours for other versions to appear and then proceeds to download best one available.

The enough parameter will specify quality that you find good enough to start
downloading without waiting whole timeframe. If qualities meeting enough parameter
and above are available, flexget will prefer the enough. Ie. if enough value is set
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