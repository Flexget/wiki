= Torrent Alive =
This plugin will reject any accepted entries that are torrents, but do not meet a minimum seed requirement. Default is to require 1 seed.

Rejections are remembered by default for one hour. If the entry is accepted again after this interval, the tracker(s) will be queried for seeds again.

'''Example:'''
{{{
torrent_alive: yes
}}}

You can also specify the minimum number of seeds needed.
{{{
torrent_alive: 10
}}}

'''Advanced Format:'''

If you need to specify that rejections should last a different amount of time than 1 hour, you can use the advanced config format:
{{{
torrent_alive:
  min_seeds: 10
  reject_for: 15 minutes
}}}