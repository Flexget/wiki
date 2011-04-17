= Inputs =
This plugin allows you to configure the same [wiki:Plugins#Inputs input plugin] multiple times in one feed. If there is an error while retrieving one of the inputs, the others will still be run.

'''Example:'''
{{{
inputs:
  - find:
      path: /home/me/incoming
      mask: '*.torrent'
  - rss: http://feeda.com
  - rss: http://feedb.com
}}}