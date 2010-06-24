= Quality =

Allows specifying acceptable qualities. All other qualities will be rejected. (NOTE: If you are using another plugin with it's own quality detection, i.e. series, you should use it's built in quality system)

''' Example: '''

{{{
quality: 1080p
}}}

This would reject all entries that are not 1080p.

If you want to specify multiple acceptable qualities it can be done like this:

{{{
quality:
  - 720p
  - 1080p
}}}

Possible values for quality are listed under [wiki:Plugins/series#Timeframe series].