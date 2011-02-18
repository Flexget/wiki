= Free Space =
This plugin will abort a feed if free space on a given drive is getting low.

{{{path}}} is the path that you want to monitor for space. [[BR]]
{{{space}}} is the amount of free space (in MB) that you require for new entries to be allowed.

'''Example'''
{{{
free_space:
  path: /location/to/monitor
  space: 500
}}}