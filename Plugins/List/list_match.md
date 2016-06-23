=== List Match ===

This is a filter plugin that uses a list to accept or reject generated entries.

== Syntax == 
{{{
list_match:
  from:
    - <list_type>: <list_name>
  [action]: [*accept*|reject]
  [remove_on_match]: [*yes*|no]
  [single_match]: [*yes*|no]
}}}

Default are marked with `*`.
