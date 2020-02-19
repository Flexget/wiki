# If
The if plugin can evaluate simple jinja expressions on the [entry fields](/Entry) and take one of several actions if the expression evaluates to True; it can accept, reject, or fail the entry, or it can run certain filter plugins on the matching entries.

## Available Objects and Functions
The if plugin allows evaluating [jinja expressions](http://jinja.pocoo.org/docs/2.9/templates/#expressions), which are similar to a limited subset of python. If statements can contain:
- All of the entry fields are available by name. If an if statement references a field that an entry does not have, the statement will automatically evaluate to false.
- [Math operators](http://jinja.pocoo.org/docs/2.9/templates/#math) are usable, e.g. + - / * and or in == < >
- [Jijna literals](http://jinja.pocoo.org/docs/2.9/templates/#literals), e.g. `true` `false` `1` `2` `'some string'` `['a', 'list, 'of', 'strings']` `{'a': 1, 'dictionary', 2}`
- Basic builtin types are also available (for casting): str unicode int float
- Any of the methods of objects available are useable with the exception of \_\_doubleunderscore\_\_ ones. e.g tvdb_genres[0].upper()
- [Jinja Filters](http://jinja.pocoo.org/docs/2.9/templates/#list-of-builtin-filters)
- [Jinja Tests](http://jinja.pocoo.org/docs/2.9/templates/#builtin-tests)
- Any of FlexGet's [custom Jinja filters/tests](/Jinja)

There are several other functions and objects available added by FlexGet. Some of them were used before the switch to jinja and have native jinja equivalents that can be switched to:


| **Object** | **Decscription** | **Jinja equivalent** |
| --- | --- | --- |
| has_field('<field_name>') | Returns true if the entry has the field field_name. | `<field_name> is defined`
| len(<iterable>) | Returns the length of the iterable | `<iterable>|length` |
| any(<iterable>) | Returns true if any of the items in the iterable are true. |
| all(<iterable>) | Returns true if all items in the iterable are true. |
| sorted(<iterable>) | Return a new sorted list from the items in iterable. | `<iterable>|sort` |
| now | This is a python datetime object equal to the time the if statement was evaluated. |
| timedelta | From the python standard library [datetime.timedelta](http://docs.python.org/library/datetime.html#datetime.timedelta) |

## Actions
### Accept, Reject, Fail
Simple actions (accept, reject, and fail) can be specified directly after the colon following the if statement.

**Example:** This will reject any series that have the 'Reality' genre, and any episodes that aired more than 10 days ago.

```
thetvdb_lookup: yes
if:
  - "'Reality' in tvdb_genres": reject
  - tvdb_ep_air_date < now - timedelta(days=10): reject
```

**Example:** Here is a more advanced example to reject multiple imdb_genres.

```
imdb_lookup: yes 

if:
  - "'Comedy' in (imdb_genres or []) and 1 == len(imdb_actors or [])": accept
```

### Run Another Filter
You can also run certain other filter plugins (and the set plugin) on matching entries. The config for the plugin should be placed on the line after the if statement with 4 more spaces.

**Example:**

Here is how might use a few plugins together to require that newer movies have a better quality than older ones.

```
imdb_lookup: yes
seen_movies: strict
quality: dvdrip+
if:
  - imdb_year > now.year - 2:
      quality: dvdrip+ 720p+
```

### Set field values
```
if:
  - "'1080p' in title":
      set:
        path: /storage/movies/1080p/
  - "'720p' in title":
      set:
        path: /storage/movies/720p/
```

Note that this example will leave path field to be undefined on entries that do not match either clause.