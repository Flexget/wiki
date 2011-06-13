= Series timeframe with min and max quality =
The [wiki:Plugins/series series] plugin supports defining a min and max quality along with [wiki:Plugins/series#Timeframe timeframe] option.
{{{
series:
  settings:
    groupa:
      min_quality: hdtv
      max_quality: 720p web-dl
      quality: 720p
      timeframe: 12 hours
  groupa:
    - The Show
}}}
 ^^^(This config snippet must be placed within a feed or a preset.)^^^
This example will download a {{{720p}}} copy of {{{The Show}}} as soon as it comes out in the feed. If a quality within the range set by min_ and max_quality comes out before a {{{720p}}} copy, the [wiki:Plugins/series series] plugin will wait {{{12 hours}}} for the {{{720p}}} version before grabbing the alternative instead.
    
