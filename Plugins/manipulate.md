= Manipulate =

Mainly for advanced users only. Allows setting and cleaning entry fields with regexp.

Syntax:

{{{
manipulate:
  <field>:
    from: <field>
    regexp: ...
}}}

=== Example ===

Title is filled with garbage that series plugin does not like.

{{{
manipulate:
  title:
    from: title
    regexp: \[\d\d\d\d\](.*)
}}}

Regexp can return any number of groups, value is combination of these (separated with space).