## [`seen`](/Plugins/seen)
View or forget entries remembered by the seen plugin
usage: flexget seen [-h] <action> ...

### Actions
| action | description |
| --- | --- |
| `forget` | Forget entry or entire task from seen plugin database |
| `add` | Add a title or url to the seen database |
| `search` | Search text from the seen database |

### Optional arguments
| argument | description |
| --- | --- |
| `-h, --help` | show this help message and exit |

### Examples
```bash
#Adds the title "The Foo Movie" to the seen database
flexget seen add "The Foo Movie"
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [`seen` Wiki article](/Plugins/seen)
