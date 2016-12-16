# Deluge Input Plugin
This plugin creates an [entry](/Entry) for each torrent that is currently loaded in Deluge (with optional filters.) It is useful for learning items you have manually added to Deluge into your FlexGet database, or changing settings (or renaming, moving) of torrents currently running in Deluge.

## Options
|  | **Main options** |
| --- | --- |
| host | Hostname or IP of Deluge daemon. (default localhost) |
| port | Port to connect to Deluge daemon. (default 58846) |
| username | Deluge username (defaults to automatic local client authentication if not specified) |
| password | Deluge password (defaults to automatic local client authentication if not specified) |
| config_path | The path to your Deluge config folder. (must be specified for .torrent files to be available) |
| filter | Criteria can be specified to limit which items from Deluge will have entries created. |
| keys | Any extra attributes that should be collected from Deluge |
|  | **Filter options** |
| label | Match torrents with the specified label. |
| state | Can be 'active', 'downloading', 'seeding', 'queued' or 'paused' |

## Entry Fields
The [entries](/Entry) that this plugin creates will have the following entry fields:

| deluge_state | Current state in Deluge, e.g. 'Downloading' |
| --- | --- |
| deluge_progress | Current percentage completed. |
| deluge_label | Label from Deluge |
| deluge_path | Deluge download location |
| deluge_movedone | Deluge move completed path |
| deluge_ratio | Deluge stop ratio |
| torrent_info_hash | The info hash for the torrent |
| torrent_seeds | The current number of seeds for the torrent |
| torrent_peers | The current number of peers for the torrent |
| torrent_private | A flag that indicates if this torrent is private |
| content_size | Size in MB of the content |
| content_files | List of the filenames in the torrent |
|  | *(the following fields are only available if `config_path` is specified)* |
| location | Path to torrent file |
||url||Path to torrent file in '!file://' format||

## Keys fields
The `keys` attribute can contain a list with any of the keys below:

`
active_time, compact, distributed_copies, download_payload_rate, file_priorities,
file_progress, is_auto_managed, is_seed, max_connections,
max_download_speed, max_upload_slots, max_upload_speed, message, move_on_completed,
next_announce, num_files, num_pieces, 
paused, peers, piece_length, prioritize_first_last, queue, remove_at_ratio, seed_rank, stop_at_ratio, stop_ratio, total_done, total_payload_download, total_payload_upload,
total_peers, total_seeds, total_uploaded, total_wanted, tracker,
tracker_host, tracker_status, trackers, upload_payload_rate
`

When any of these keys are present, the entry will get populated with these values from Deluge