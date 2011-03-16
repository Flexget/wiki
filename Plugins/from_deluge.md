= Deluge Input Plugin =
This plugin creates an [wiki:Entry entry] for each torrent that is currently loaded in Deluge (with optional filters.) It is useful for learning items you have manually added to Deluge into your !FlexGet database, or changing settings (or renaming, moving) of torrents currently running in Deluge.

== Options ==
||'''Main options'''||
||host||Hostname or IP of Deluge daemon. (default localhost)||
||port||Port to connect to Deluge daemon. (default 58846)||
||user||Deluge username (defaults to automatic local client authentication if not specified)||
||pass||Deluge password (defaults to automatic local client authentication if not specified)||
||config_path||The path to your Deluge config folder. (must be specified for .torrent files to be available)||
||filter||Criteria can be specified to limit which items from Deluge will have entries created.||
||'''Filter options'''||
||label||Match torrents with the specified label.||
||state||Can be 'active', 'downloading', 'seeding', 'queued' or 'paused'||