= Inputs =
This plugin allows you to configure the same [wiki:Plugins#Inputs input plugin] multiple times in one task.

'''Notes:'''
- If entries with duplicate titles or urls are found, only the first one seen will be added to the task.
- If there is an error while retrieving one of the inputs, the others will still be run.

'''Example:'''
{{{
inputs:
  - find:
      path: /home/me/incoming
      mask: '*.torrent'
  - rss: http://feeda.com
  - rss: http://feedb.com
}}}