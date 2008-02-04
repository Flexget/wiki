= Series (not finished yet) =

Intelligent filter for tv-series. This solves duplicate downloads problem that occurs when using patterns (regexp) matching since same episode is often released by multiple groups.

Example configuration:

{{{
series:
  - some series
  - another series
}}}          

If "some series" and "another series" have understandable episode
numbering entry is downloaded only once.

So if we get same episode twice:
        
 * Some.Series.S2E10.More.Text
 * Some.Series.S2E10.Something.Else

Only first file is downloaded. TODO: or actually the one with better quality ...

== Advanced usage ==

In case of multiple different qualities, user may wish to specify timeframe after which best quality is downloaded. More configuration options coming in future ...

Example:

{{{
series:
  - awesome series:
      best_in: 6
}}}

This would download best quality that appears in 6 hours from first occurrence of episode.



== Ideas to be implemented ==

Accept immediately instead of waiting if quality is expected

{{{
series:
  - awesome series:
      best_in:
        hours: 6
        immediately_if: 
         - hdtv
         - 720p
  - another series
}}}

Accept only listed qualities

{{{
series:
  - awesome series:
      quality:
        - hdtv
        - 720p
  - another series
}}}

Do not download older episodes than ..

{{{
series:
  - awesome series:
      - min_ep: S05E12
}}}