# Trakt CLI tools
There are multiple trakt plugins that may need authentication to your trakt account (i.e. if the profile/list is private, or if you are trying to edit lists.) Any such plugin will have an `account` option. The [`flexget trakt` CLI command](/CLI/trakt) can be used to store that authentication under a given account name. Once you have set authentication up with this tool, you can set the `account` option in the appropriate trakt plugins to use this authentication.

The `username` option will also be available alongside `account` option in trakt plugins. This option is not required when using an authenticated account, as it will default to the account owner. You can specify a different username than the account owner however (e.g. to specify a friend's username who has shared permissions with you.)

## Usage
Call the [trakt CLI](/CLI/trakt) command with `flexget trakt` and one of the following subcommands:

### auth
Takes one argument, `account`. This will be the account name you use in the trakt plugin configs. This will give you a url and code to type in to that page in order to authorize your account, and will wait for you to do so before storing the authorization.

`flexget trakt auth <account>`. This command generates an `access_token`, which grants Flexget access to your Trakt.tv account. An `access_token` is valid for 3 months after which Flexget will automatically generate a new `access_token`.

If something should go wrong, you can run the command again and update your authorization.

**We strongly recommend that you use your Trakt.tv username as `account` name to avoid confusion down the line.**

### refresh
Takes one argument `account`; the name you chose when authorizing Flexget to access your Trakt.tv account. Issuing `flexget trakt refresh <account>` will manually refresh the current `access_token` -- this command is not necessary as Flexget should automatically request a new `access_token` once it expires.

### show
Takes an optional argument `account`, which shows the expiration date for the current `access_token`. If `account` is not specified, it lists all saved accounts along with their `access_token` creation dates and expiration dates.

### delete
Takes a required argument `account`; This deletes the given account data from the Flexget database.

**Please Note**: This will not revoke access from your Trakt.tv account. You must do that from the [Trakt.tv](http://trakt.tv/oauth/authorized_applications) website.