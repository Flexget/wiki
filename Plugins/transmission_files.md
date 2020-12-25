# Transmission Files
This plugin creates an entry for each file within the torrents you have loaded in transmission.

This plugin requires the transmission-rpc library. To install it, run:

```
pip install transmission-rpc
```

You may be required to upgrade transmission-rpc after upgrading transmission, for that just add `--upgrade` to the previous command.

**Example:**

```
transmission_files:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
```


| **Name** | **Info** | **Description** |
| --- | --- | --- |
| host | Text | Where transmission is listening (default: localhost) |
| port | Number | Connected port (default: 9091) |
| netrc | File |  |
| username | Text |  |
| password | Text |  |
| onlycomplete | [yes|no](/yes|no) | If this is enabled, only completed files will have entries created. |
|  torrent_info_hash  |  List or String  |  Info hash(es) of the torrent(s) to list the contents of. Will list all torrents if no hashes provided.  |
