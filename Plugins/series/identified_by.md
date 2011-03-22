== Identified by ==

Specify how episode number is detected.

'''Example:'''

{{{
series:
  - test:
      identified_by: id
}}}

Possible values: `ep`, `id`, `auto`

Default value is `auto` which uses episode history to detect what to use. In absence of reliable history both `ep` and `id` format are accepted.
