= Commandline Config =

'''NOT IMPLEMENTED. See #20'''

Module that allows passing configuration values from commandline parameter.

Keywords in configuration file:

{{{
feeds:
  some_rss:
    rss: @url
    download: @path
}}}

Commandline:

{{{
  --options "url=http://something, path=~/download"
}}}


Implementation idea:

 * builtin module, so that does not require setting it in for each feed.
 * register new commandline parameter, --options
 * hook event start
 * on start event iterate trough feed.config (dict, recursively) and replace all variables with ones specified in commandline