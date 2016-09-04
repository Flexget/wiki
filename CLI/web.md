## `web`
Manage web server settings

### Positional arguments
| argument | option | description |
| --- | --- | --- |
| `passwd` | change password for web server |
|| `<new password>` | New password |
| `gentoken` | Generate a new api token |
| `showtoken` | Show api token |

### Examples
```bash
#shows the flexget web server API token
flexget web showtoken
#changes the password to foopass
flexget web passwd foopass
```

### Related articles
* [CUI / Command line interface overview](/CLI)