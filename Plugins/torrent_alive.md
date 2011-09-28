= Torrent Alive =
This plugin will reject any accepted entries that are torrents, but do not have at least 1 seed on at least one of their trackers.

Rejections are remembered for one hour. If the entry is accepted again after this interval, the tracker(s) will be queried for seeds again.

'''Example:'''
{{{
torrent_alive: yes
}}}