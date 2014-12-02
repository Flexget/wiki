= Qualities =

This option can be used if you want to allow multiple qualities of the same episode of a series. The option takes a list of [wiki:Qualities#Requirements quality requirements]. A maximum of one release can be accepted that matches each line you specify for this option. One release may satisfy the requirements of multiple lines you have specified.

== Example ==

{{{
series:
  - name of the series:
      qualities:
        - 720p webdl
        - hdtv <720p
}}}

== Use with upgrade ==

The same rules apply when this is combined with the [wiki:Plugins/series/upgrade upgrade] option, however, no releases will be downloaded which are considered a lower quality than one which has already been grabbed, even if it qualifies for another requirement in your qualities list.

== Use with timeframe ==

`qualities` can be used with the [wiki:Plugins/series/timeframe timeframe] option, instead of defining a `target`. Any of the qualities you define here will be accepted immediately. If none of the qualities you list here are available within the timeframe, another release will be accepted. Your defined qualities will continue to be looked for even after the timeframe has expired and a backup release has been grabbed.