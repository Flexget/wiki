## `trakt`
View and manage trakt authentication

### Actions
| action | option | description |
| --- | --- | --- |
| `auth` || Authorize Flexget to access your Trakt.tv account |
|| *positional:* |
|| `<account>`| Local identifier which should be used in your config to refer these credentials
| `list` || List expiration date for Flexget authorization(s) (don't worry, they will automatically refresh when expired) |
|| *positional:* |
|| `<account>`| Local identifier which should be used in your config to refer these credentials
|| *optional:* |
|| `--table-type {plain,porcelain,github,single,double}` | Select output table style |
|| `--porcelain` | Make the output parseable. Similar to using `--table-type porcelain`|
| `refresh` | Manually refresh your access token associated with your `--account <name>` |
|| *positional:* |
|| `<account>`| Local identifier which should be used in your config to refer these credentials
| `delete` | Delete the specified <account> name from local database |
|| *positional:* |
|| `<account>`| Local identifier which should be used in your config to refer these credentials

### Examples
```bash
#refreshes the access token associated with the "my_foo_account"
flexget trakt refresh account my_foo_account
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [trakt Plugin](/Plugins/trakt)