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

If "some serie" and "another serie" have understandable episode
numbering any given episode is downloaded only once.

So if we get same episode twice:

Some.Serie.S2E10.More.Text[[BR]]
Some.Serie.S2E10.Something.Else

Only first file is downloaded.

If two different qualities come available at the same moment,
flexget will always download the better one. (more options coming ..)

== Timeframe ==

Series filter allows you to specify a timeframe for each serie in which
flexget waits better quality.

'''Example configuration:'''

{{{
series:
  - some serie:
      timeframe:
        hours: 4
        enough: 720p
  - another serie
  - third serie
}}}

In this example when a epsisode of 'some serie' appears, flexget will wait
for 4 hours incase and then proceeds to download best quality available.

The enough parameter will tell the quality that you find good enough to start
downloading without waiting whole timeframe. If qualities meeting enough parameter
and above are available, flexget will prefer the enough. Ie. if enough value is set
to 'hdtv' and qualities dsk, hdtv and 720p are available, hdtv will be chosen.
If we take hdtv off from list, 720p would be downloaded.

Enough has default value of 720p.

Possible values for enough (in order): 1080p, 1080, 720p, 720, hr, dvd, hdtv, dsr, dsrip