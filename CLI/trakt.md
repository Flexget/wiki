## `trakt`
View and manage trakt authentication

### Actions
| action | description |
| --- | --- |
| `auth` | Authorize Flexget to access your Trakt.tv account |
| `list` | List expiration date for Flexget authorization(s) (don't worry, they will automatically refresh when expired) |
| `refresh` | Manually refresh your access token associated with your `--account <name>` |
| `delete` | Delete the specified <account> name from local database |

### Examples
```bash
#refreshes the access token associated with the "my_foo_account"
flexget trakt refresh --account my_foo_account
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [trakt Plugin](/Plugins/trakt)