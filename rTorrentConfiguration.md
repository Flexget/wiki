# Example rTorrent configuration
```
# where transfers are stored
directory = /storage/torrents/transfering/

# watch directories, and final location once completed
schedule = watch_directory_1,10,10,"load_start=~/torrents/movies/*.torrent,d.set_custom1=/storage/torrents/movies/"
schedule = watch_directory_2,10,10,"load_start=~/torrents/series/*.torrent,d.set_custom1=/storage/torrents/series/"
schedule = watch_directory_3,10,10,"load_start=~/torrents/misc/*.torrent,d.set_custom1=/storage/torrents/misc/"
schedule = watch_directory_4,10,10,"load_start=~/torrents/anime/*.torrent,d.set_custom1=/storage/torrents/anime/"
schedule = watch_directory_5,10,10,"load_start=~/torrents/jpop/*.torrent,d.set_custom1=/storage/torrents/jpop/"

# On completion, move the torrent to the directory from custom1.
on_finished = move_complete,"execute=mv,-u,$d.get_base_path=,$d.get_custom1= ;d.set_directory=$d.get_custom1="
```

For rTorrent 0.8.4-> you need to replace the last line with this one

```
system.method.set_key = event.download.finished,move_complete,"execute=mv,-u,$d.get_base_path=,$d.get_custom1= ;d.set_directory=$d.get_custom1="
```
