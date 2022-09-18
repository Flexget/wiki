---
title: trakt
description: 
published: true
date: 2022-09-18T05:25:34.631Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:44.654Z
---

## [CLI](/CLI) > `trakt`
View and manage [Trakt authentication](/Trakt_Authentication), for use with the [`trakt_list`](/Plugins/List/trakt_list) and [`trakt_lookup`](/Plugins/trakt_lookup) plugins.

### Sub-commands
| Sub-command | Option | Description |
| --- | --- | --- |
| `auth` || Authorize Flexget to access your Trakt.tv account. This argument generates an `access_token` which grants Flexget access to your Trakt.tv account. An `access_token` is valid for 3 months after which Flexget will automatically generate a new `access_token`. It can be manually refreshed using the `refresh` argument below.|
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
{{> Includes/TableStylesDiv }}

### Examples
```bash
#refreshes the access token associated with the "my_foo_account"
$ flexget trakt refresh my_foo_account
```