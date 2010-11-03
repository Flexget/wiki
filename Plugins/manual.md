= Manual =

Any feeds that have this plugin enabled will not be run unless they are explicitly called with the [wiki:Plugins/--feed --feed] plugin.

'''Example:'''
{{{
feeds:
  thefeed:
    manual: yes
}}}
!FlexGet will not execute {{{thefeed}}} unless you run it with the command {{{flexget --feed thefeed}}}