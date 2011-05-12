= Timeframe =

Specify a timeframe in which !FlexGet waits for the chosen quality. The desired quality should be given with [wiki:Plugins/series/quality quality] directive. If specified quality does not become available within given timeframe after a different quality has been seen, best quality so far is chosen. `Quality` has default value of 720p when timeframe option is given.

'''Example:'''

{{{
series:
  - some series:
      timeframe: 4 hours
      quality: 720p
  - another series
  - third series
}}}

Timeframe value: NUM (minutes|hours|days|weeks)

=== Behavior with Min and Max Quality Options ===
If [wiki:Plugins/series/quality min_quality] or [wiki:Plugins/series/quality max_quality] is also defined, they will define the minimum and maximum quality for episodes when timeframe has expired. (Before the timeframe has expired, only the quality defined with the {{{quality}}} option will be accepted.)

=== Behavior with Qualities Option ===
If the [wiki:Plugins/series/quality qualities] option is defined alongside timeframe, the timeframe will only kick in if ''none'' of your defined qualities have been downloaded within the timeframe.
