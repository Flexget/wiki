= Series (not finished yet) =

Intelligent filter for tv-series. This solves duplicate downloads problem that occurs when using patterns (regexp) matching since same episode is often released by multiple groups.

Example configuration:

{{{
series:
  - some serie
  - another serie
}}}          

If "some serie" and "another serie" have understandable episode
numbering entry is downloaded only once.

So if we get same episode twice:
        
 * Some.Serie.S2E10.More.Text
 * Some.Serie.S2E10.Something.Else

Only first file is downloaded. TODO: or actually the one with better quality ...

== Advanced usage ==

In case of multiple different qualities, user may wish to specify timeframe after which best quality is downloaded. More configuration options coming in future ...

Example:

{{{
series:
  - awesome serie:
      best_in: 6
}}}

This would download best quality that appears in 6 hours from first occurrence of episode.
