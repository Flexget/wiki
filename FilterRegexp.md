== Regexp (documentation under work !!) ==

Use regular expression to Accept, Filter or Reject entries. !FlexGet uses python regexp format and all matching is done case insensitive. This module may look a bit scary but in reality you rarely want anything more than what simple examples describe.

=== Simple examples ===

Accept entries matching regexp(s) and filter rest of the entries.

{{{
regexp:
  accept:
    - pattern
  rest: filter
}}}

Filter entries matching regexp(s), they can still be accepted by other filters.

{{{
regexp:
  filter:
    - pattern
}}}

Reject (irreversibly) entries matching regexp(s). This should be used when you never want to download matching entries, even if some other module (ie. FilterImdb) deems them acceptable.

{{{
regexp:
  reject:
    - pattern
}}}

== Set custom path ==

Any regexp rule can set custom path for matching entry.

=== Example ===

{{{
regexp:
  accept: 
    - pattern: ~/custom/path
  rest: filter
}}}

or

{{{
regexp:
  accept: 
    - pattern:
        path: ~/custom/path
  rest: filter
}}}

== Full syntax ==

{{{
regexp:
  <operation>:
    - pattern 1
    - pattern 2: <custom path>
    - pattern 3:
        [not]:
          - pattern 4
        [path]: <custom path>
  [rest]: <operation>
}}}

Available operations: {{{accept, filter, reject, accept_excluding, filter_excluding and reject_excluding}}}.
Rest and not parameters are optional. Configuration may contain any number and combination of different operations.