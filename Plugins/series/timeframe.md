= Timeframe and Target =

Timeframe value: NUM (minutes|hours|days|weeks)

Specify a timeframe in which !FlexGet waits for the chosen quality. The desired quality should be given with {{{target}}} option, and should be a valid [wiki:Qualities#Requirements quality requirements] string. If specified quality does not become available within given timeframe after a different quality has been seen, best quality so far is chosen. `target` has default value of 720p hdtv+ when timeframe option is given. 

If you also specify the [wiki:Plugins/series/quality quality] option along with timeframe, it will be enforced no matter what (both before and after the timeframe expires.)

'''Example:'''

Wait for 720p hdtv release for 4 hours, if not available in that timeframe accept best episode seen, can be lower OR higher in quality.

{{{
series:
  - some series:
      timeframe: 4 hours
      target: 720p hdtv
  - another series
  - third series
}}}

'''Example:'''

Wait for 12 hours for 1080p webdl and after that fall back to anything between 720p-1080p in resolution from webdl source.

{{{
series:
  - some series:
      timeframe: 12 hours
      target: 1080p webdl
      quality: 720p-1080p webdl
}}}

=== Behavior with qualities option ===

If the [wiki:Plugins/series/quality qualities] option is defined alongside timeframe, the timeframe will only kick in if ''none'' of your defined qualities have been downloaded within the timeframe.
