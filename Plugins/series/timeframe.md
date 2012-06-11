= Timeframe =

Specify a timeframe in which !FlexGet waits for the chosen quality. The desired quality should be given with {{{enough}}} option, and should be a valid [wiki:Qualities#Requirements quality requirements] string. If specified quality does not become available within given timeframe after a different quality has been seen, best quality so far is chosen. `enough` has default value of 720p when timeframe option is given. If you also specify the [wiki:Plugins/series/quality quality] option along with timeframe, it will be enforced no matter what (both before and after the timeframe expires.)

'''Example:'''

{{{
series:
  - some series:
      timeframe: 4 hours
      enough: 720p+ hdtv+
  - another series
  - third series
}}}

Timeframe value: NUM (minutes|hours|days|weeks)

=== Behavior with Qualities Option ===
If the [wiki:Plugins/series/quality qualities] option is defined alongside timeframe, the timeframe will only kick in if ''none'' of your defined qualities have been downloaded within the timeframe.
