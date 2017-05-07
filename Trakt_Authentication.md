# Trakt Authentication
There are multiple Trakt plugins (such as [`trakt_list`](/Plugins/List/trakt_list), [`list_remove`](/Plugins/List/list_remove), [`trakt_lookup`](/Plugins/trakt_lookup), and [`list_clear`](/Plugins/List/list_clear)) that need to authenticate with your Trakt account if the profile or list is private, or if you are trying to edit lists. Any such plugin will have an `account` option.

The [`flexget trakt` CLI command](/CLI/trakt) can be used to store that authentication under a given account name. Once you have set authentication up with this tool, you can set the `account` option in the appropriate Trakt plugins to access private information or edit lists.

The `username` option is also available in trakt plugins. This option is used for two purposes:
- To access public information from the given username (such as public lists)
- To specify a user that is _different_ from the `account` option, such as a friend's username who has shared permissions with you.

If you are using the `account` option, it is not required as it will default to the `account`'s user.

## Authenticating with Trakt

### Initial authentication
To authenticate with Trakt for the first time, run the following [CLI](/CLI/trakt) command:
```bash
$ flexget trakt auth <account>
```

`<account>` will be the account name you use in the Trakt plugin configurations. While it has nothing to do with the Trakt account that is being authorized, and therefore doesn't have to be the same as your Trakt username, it is **strongly recommended** that you use your Trakt username to avoid confusion later.

Running this command will give you a URL to go to and a code to type in on that page to authorize your account. It will wait for you to do so. When this is done, an `access_token` is generated and stored.

If something should go wrong, you can run the command again and update your authorization.

### Refreshing the `access_token`

If you wish to manually refresh your token, you can do using the `refresh` argument.
```bash
$ flexget trakt refresh <account>
```
`<account>` is the account name you chose when originally authenticating FlexGet with Trakt. Issuing this command will manually refresh the current `access_token`. Generally this command is not necessary as Flexget should automatically request a new `access_token` once it expires.

### Review existing accounts

Use the `list` argument to see what authorizations FlexGet has stored as well as their `access_token` expiration dates.
```bash
$ flexget trakt list <account>
```
`<account>` is optional here and if specified will show only that account's details. Otherwise, all authorizations will be displayed.

### Delete account from FlexGet
The `delete` argument lets you remove an account from FlexGet. Note this **does not revoke access on the Trakt side** - to do that, you must visit the  [trakt.tv](https://trakt.tv/oauth/authorized_applications) website.

This argument requires an `account` be listed. You cannot delete all accounts at once.
```bash
$ flexget trakt delete <account>
```