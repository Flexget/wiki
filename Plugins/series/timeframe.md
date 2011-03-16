== Timeframe ==

Specify a timeframe in which !FlexGet waits for a chosen quality. The desired quality can be given with `quality` directive. If specified quality does not come available within timeframe best quality so far is chosen. `Quality` has default value of 720p when timeframe option is given.

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
