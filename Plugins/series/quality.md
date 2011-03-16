== Quality ==

||'''Name'''||'''Description'''||
||quality||Accept only given quality. No other quality will be accepted.||
||min_quality||Accept only qualities equal or above this^*^||
||max_quality||Accept only qualities equal or below this^*^||
||qualities||Accept all given qualities, multiple downloads^*^||

^* = Does not work with [#Timeframe timeframe] (but there is a [wiki:Cookbook/Series/TimeframeWithMinMaxQuality workaround])^

Possible values for quality can be found [wiki:Plugins/quality#KnownQualities here.]

'''Example:'''

{{{
series:
  - name of series 1:
      quality: 720p
  - name of series 2:
      min_quality: hr
      max_quality: 720p
  - name of series 3:
      qualities:
        - pdtv
        - 720p
}}}

Usually best way to specify quality for series is to use groups:

'''Example:'''

{{{
series:
  720p:
    - name of series 1
    - name of series 2
  hdtv:
    - name of series 3
    - name of series 4
}}}

See [wiki:Plugins/series#Groupsettings groups] for more information.
