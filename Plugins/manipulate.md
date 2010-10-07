= Manipulate =

Mainly for advanced users only. Allows setting and cleaning entry fields with regexp.

For revisions prior r1395 see [wiki:Plugins/manipulate?version=8 older version].

Syntax:

{{{
manipulate:
  - <destination field>:
      [event]: <event>
      [from]: <source field>
      [extract]: <regexp>
      [replace]:
        regexp: <regexp>
        format: <regexp>
}}}

=== Example 1 ===

Title is filled with garbage that series plugin does not like.

eg.

{{{
[48952] The Series S01E01 720p
}}}

This could be fixed by removing the [48952]

{{{
manipulate:
  - title:
      extract: \[\d\d\d\d\](.*)
}}}

Regexp can return any number of groups, value is combination of these (separated with a space).

=== Example 2 ===

Some badly written site has invalid URLs. Uses &amp; instead of &

{{{
manipulate:
  - url:
      replace:
        regexp: '&amp;'
        format: '&'
}}}

Starting from r1420 these are fixed automatically by [wiki:Plugins/urlfix urlfix] plugin.

=== Example 3 ===

You can do multiple manipulates in a row, and they will be executed in order. You can also do multiple manipulates on the same field.

{{{
manipulate:
  - title:
      extract: .*\[\s*(.*)\s*\]-.*
  - filename:
      from: title
  - title:
      replace:            
        regexp: '[\.-]'
        format: ' '
}}}

=== Example 4 ===

You can control how the regex hits are output using \1, \2, etc in format.

{{{
manipulate:
  - title:
      replace:            
        regexp: '(.*)/(.*)/(.*)'
        format: '\2.\1.\3'
}}}