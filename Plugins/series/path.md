== Override path ==

Specify a custom path for a series. Note that this does '''not''' download it, your feed must have output plugin (eg. [wiki:Plugins/download download], [wiki:Plugins/deluge deluge])

'''Example:'''

{{{
series:
  - some series:
      path: ~/download/some_series/
  - another series
  - third series
download: ~/download/
}}}

Series {{{another series, third series}}} will be downloaded into {{{~/downloads}}}. However {{{some series}}} has overridden path and will be downloaded into {{{~/downloads/some_series/}}}.

It's also possible to set path globally from series name with [wiki:Plugins/set set] plugin, see [wiki:Cookbook/SetPath this recipe].