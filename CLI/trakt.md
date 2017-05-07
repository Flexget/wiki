## `trakt`
View and manage Trakt authentication.

### Actions
| Argument | Option | Description |
| --- | --- | --- |
| `auth` || Authorize Flexget to access your Trakt account. This argument generates an `access_token` which grants Flexget the ability to access private information, such as collections and views. An `access_token` is valid for 3 months after which Flexget will automatically generate a new `access_token`. It can be manually refreshed using the `refresh` argument below.|
|| *positional:* |
|| `<account>`| Identifier which will be used in your config (and other commands on this page) to refer to these credentials. This is specific to FlexGet and does not affect your trakt.tv account, _but_ it is strongly recommended that you use your trakt.tv username to avoid confusion later.
| `list`* || List expiration date for FlexGet authorizations. (Don't worry, they will automatically refresh when expired.) |
|| *positional:* |
|| `<account>`| Identifier (as originally specified with the `auth` command above)
| `refresh` || Manually refresh the access token associated with your identifier |
|| *positional:* |
|| `<account>`|Identifier (as originally specified with the `auth` command above)
| `delete` || Delete the specified identifier from local database |
|| *positional:* |
|| `<account>`| Identifier (as originally specified with the `auth` command above)
|||<div align="right">\* supports [table-styles](/CLI/--table-styles)</div>

### Examples
```bash
#refreshes the access token associated with the "my_foo_account"
flexget trakt refresh my_foo_account
```

### Related articles
* [Trakt Authentication](/Trakt_Authentication)
* [CLI / Command line interface overview](/CLI)
* [`trakt_list` list plugin](/Plugins/List/trakt_list)
* [`list_remove` list plugin](/Plugins/List/list_remove) 
* [`trakt_lookup` plugin](/Plugins/trakt_lookup)
* [`list_clear` list plugin](/Plugins/List/list_clear)