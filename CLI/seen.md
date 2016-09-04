## [`seen`](/Plugins/seen)
View or forget entries remembered by the seen plugin
usage: flexget seen [-h] <action> ...

### Actions
| action | option | description |
| --- | --- | --- |
| `forget` | Forget entry or entire task from seen plugin database |
|| `<value>` |  Title or url of entry to forget, or name of task to forget |
| `add` | Add a title or url to the seen database |
|| `<value>` | the title or url to add |
| `search`* | Search text from the seen database |
|| `<search term>` | term to search for |
|<div align="right">\* supports [table-styles](/CLI/--table-styles)</div>

### Examples
```bash
#Adds the title "The Foo Movie" to the seen database
flexget seen add "The Foo Movie"
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [`seen` Wiki article](/Plugins/seen)
