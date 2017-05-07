## [CLI](/CLI) > `web`
Manage web server settings

### Positional arguments
| Argument | Option | Description |
| --- | --- | --- |
| `passwd` || change password for web server |
|| `<new_password>` | New password |
| `gentoken` || Generate a new api token |
| `showtoken` || Show api token |

### Examples
```bash
#shows the FlexGet web server API token
$ flexget web showtoken

#changes the password to foopass
$ flexget web passwd foopass
```