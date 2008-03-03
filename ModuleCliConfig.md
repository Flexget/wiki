= Commandline config =

Allows specifying yml configuration values from commandline parameters.

Yml variables are prefixed with dollar sign ($).
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