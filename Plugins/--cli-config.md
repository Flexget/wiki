= Commandline config =

Allows specifying configuration values from commandline parameters.

Commandline values are specified in YAML by variable prefixed with dollar sign ($).
Commandline parameter must be comma separated list of variable=values.

Configuration example:

{{{
feeds:
  my feed:
    rss: $url
    download: $path
}}}

Commandline example:

{{{
--cli-config "url=http://some.url/, path=~/downloads"
}}}