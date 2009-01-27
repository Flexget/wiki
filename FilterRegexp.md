== Regexp (documentation under work !!) ==

Use regular expression to Accept, Filter or Reject entries. !FlexGet uses python regexp format and all matching is done case insensitive.

=== Example ===

Accept entries matching regexp and filter rest of the entries.

{{{
regexp:
  accept:
    - pattern
  rest: filter
}}}

=== Example ===

Filter entries matching regexp, they can still be accepted by other filters.

{{{
regexp:
  filter:
    - pattern
}}}

=== Example ===

Reject (irreversibly) entries matching regexp. This should be used when you never want to download entries with this, even if they are acceptable by other modules.

{{{
regexp:
  reject:
    - pattern
}}}

== Full syntax ==

{{{
regexp:
  <operation>:
    - pattern 1
    - pattern 2: <custom path>
    - pattern 3:
        not:
          - pattern 4
        path: <custom path>
  [rest]: <operation>
}}}

Available operations: {{{accept, filter, reject, accept_excluding, filter_excluding and reject_excluding}}}.
Rest parameter is optional. Configuration may contain any number and combination of different operations.