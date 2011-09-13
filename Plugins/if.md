= If =

The if plugin can evaluate simple python expressions on the [wiki:Entry entry fields] and take one of several actions if the expression evaluates to True; it can accept, reject, or fail the entry, or it can run certain filter plugins on the matching entries.

== Available Objects and Functions ==

The if plugin allows a limited subset of python. If statements can contain:
- All of the entry fields are available by name. If an if statement references a field that an entry does not have, the statement will automatically evaluate to false.
- All python operators are usable, e.g. + - / * and or in == < >
- Python literals, e.g. True False 1 2 'some string' ['a', 'list, 'of', 'strings'] {'a': 1, 'dictionary', 2}
- Basic builtin types are also available (for casting): str unicode int float
- Any of the methods of objects available are useable with the exception of !__doubleunderscore!__ ones. e.g series_genres![0].upper()
- There are several other functions and objects available:
||'''Object'''||'''Decscription'''||
||has_field('<field_name>')||Returns true if the entry has the field field_name.||
||len(<iterable>)||Returns the length of the iterable||
||any(<iterable>)||Returns true if any of the items in the iterable are true.||
||all(<iterable>)||Returns true if all items in the iterable are true.||
||now||This is a python datetime object equal to the time the if statement was evaluated.||
||timedelta||From the python standard library [http://docs.python.org/library/datetime.html#datetime.timedelta datetime.timedelta]||

== Actions ==
=== Accept, Rejcet, Fail ===

Simple actions (accept, reject, and fail) can be specified directly after the colon following the if statement.

'''Example:''' This will reject any series that have the 'horror' genre, and any episodes that aired more than 10 days ago.

{{{
thetvdb_lookup: yes
if:
  - "'Reality' in series_genres": reject
  - ep_air_date < now - timedelta(days=10): reject
}}}

'''Example:''' Here is a more advanced example to reject multiple imdb_genres.

{{{
imdb_lookup: yes
if:
  - "any(genre in ['horror', 'documentary'] for genre in imdb_genres)": reject
}}}

=== Run Another Filter ===

You can also run certain other filter plugins (and the set plugin) on matching entries. The config for the plugin should be placed on the line after the if statement with 4 more spaces.

'''Example:'''

Here is how might use a few plugins together to require that newer movies have a better quality than older ones.

{{{
imdb_lookup: yes
seen_movies: strict
quality:
  min: dvdrip
if:
  - imdb_year > now.year - 2:
      quality:
        min: 720p
}}}

=== Set field values ===

{{{
if:
  - "'1080p' in title":
      set:
        path: /storage/movies/1080p/
  - "'720p' in title":
      set:
        path: /storage/movies/720p/
}}}

Note that this example will leave path field to be undefined on entries that do not match either clause.