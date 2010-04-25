= Manipulate =

Mainly for advanced users only. Allows setting and cleaning entry fields with regexp.

For revisions prior r1274 see [wiki:Plugins/manipulate?version=3 older version].

Syntax:

{{{
manipulate:
  <destination field>:
    [from]: <source field>
    [extract]: <regexp>
    [replace]:
      regexp: <regexp>
      format: <regexp>
}}}

=== Example 1 ===

Title is filled with garbage that series plugin does not like.

{{{
manipulate:
  title:
    extract: \[\d\d\d\d\](.*)
}}}

Regexp can return any number of groups, value is combination of these (separated with a space).

== Example 2 ===

Some badly written site has invalid URLs. Uses &amp; instead of &

{{{
manipulate:
  url:
    replace:
      regexp: &amp;
      format: &
}}}
