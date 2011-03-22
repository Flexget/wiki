= Episode numbering matching =

ep_regexp is for series enumerated by season and episode numbers (eg, S04E01). Naive example:

{{{
ep_regexp:
  - s(\d+)e(\d+)
  - s(\d+)ep(\d+)
}}}

id_regexp is for series that are not enumerated by season/episode numbering. Naive example:

{{{
id_regexp:
  - (\d\d\d\d).(\d+).(\d+)
  - (\d+).(\d+).(\d\d\d\d)
}}}

User defined regexps takes priority over the built-in expressions.

Specifying `ep_regexp` disables all `id_regexp`'s and vice versa.
