## Archive
The archive plugin will keep a history of all entries from a given task, whether they have been accepted or not. This archive can then later be searched, and entries injected into a task again.


Simply enable without any tagging.

```
archive: yes
```

With tagging:

```
archive: [torrent, tv]
```

Search (via commandline):

```
archive search [@TAG] [@TAG] KEYWORD
```
Note: if keyword has spaces it must be quoted.

Retrieve and inject into task (via commandline):

```
archive inject ID [FORCE]
```
For more examples and complete commandline/CLI usage see the [CLI archive](/CLI/archive) article.

## Urlrewriter
```
flexget_archive: yes
```

or

```
flexget_archive: [tag, tag]
```

This works with [discover](/Plugins/discover) and also with urlrewriting but has less use in there.

## See also
- [`flexget_archive` as search plugin for `discover`](/Searches/flexget_archive)