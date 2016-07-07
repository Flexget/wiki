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