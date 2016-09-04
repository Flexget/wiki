## [`seen`](/Plugins/seen)
View or forget entries remembered by the seen plugin
usage: flexget seen [-h] <action> ...

### Actions
| action | option | description |
| --- | --- | --- |
| `forget` || Forget entry or entire task from seen plugin database |
|| `<value>` |  Title or url of entry to forget, or name of task to forget |
| `add` || Add a title or url to the seen database |
|| `<value>` | the title or url to add |
| `search`* || Search text from the seen database |
|| `<search term>` | term to search for |
|<div align="right">\* supports [table-styles](/CLI/--table-styles)</div>

### Examples
```bash
#Adds the title "The Foo Movie" to the seen database
flexget seen add "The Foo Movie"
#Can be used to forget everything seen from the FooTask.
flexget seen forget FooTask
#Can be used to remove any url, title or even imdb url which already has been seen once to be downloaded again
flexget seen forget <value>
#Can can be used to add any url, title or even imdb url as already seen  preventing them to be downloaded
flexget seen add <value>
#Especially useful when you have downloaded something manually outside FlexGet
seen add "http://example.com/torrents/1235321"
#With tasks using plugin seen_movies you can also use imdb id to mark any movie as already seen
flexget seen add tt0119698
#If you want to remove manually added "seen" things
flexget seen --forget "--seen"
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [`seen` Wiki article](/Plugins/seen)
* The [`execute` option](/CLI/execute) `--learn` (optionally combined with `--tasks`) can be used to mark all entries that would be accepted as seen.
