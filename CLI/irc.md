## `irc`
View and manage irc connections

### Actions
| action | option | description |
| --- | --- | --- |
| `status` | Shows status for specific irc connection |
|| *positional:* ||
|| `irc_connection` | Title of the irc connection |
| `restart` || Restart an irc connection |
|| *positional:* ||
|| `irc_connection` | Title of the irc connection |
| `stop` || Stops an irc connection |
|| *positional:* ||
|| `irc_connection` | Title of the irc connection |


### Examples
```bash
#shows the status for a specific irc connection
flexget irc status
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [IRC plugin](/Plugins/Daemon/irc)