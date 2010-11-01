= Series timeframe with min and max quality =
The [wiki:Plugins/series series] plugin does not support defining a min and max quality when using the [wiki:Plugins/series#Timeframe timeframe] option. This can worked around by using the [wiki:Plugins/quality quality] plugin in conjunction with the [wiki:Plugins/series series] plugin.
{{{
quality:
  min: hdtv
  max: 720p web-dl
series:
  settings:
    groupa:
      quality: 720p
      timeframe: 12 hours
  groupa:
    - The Show
}}}
 ^^^(This config snippet must be placed within a feed or a preset.)^^^
This example will download a {{{720p}}} copy of {{{The Show}}} as soon as it comes out in the feed. If a quality within the range set by the [wiki:Plugins/quality quality] plugin comes out before a {{{720p}}} copy, the [wiki:Plugins/series series] plugin will wait {{{12 hours}}} for the {{{720p}}} version before grabbing the alternative instead.
    
