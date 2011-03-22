== Advanced matching with regexps ==

The standard name matching is not perfect, some times you may need to specify regexp(s) manually. Usually the `name_regexp`.

'''Notes:'''
 
 * Use this only if you're having problems with matching, it should be able to handle 99% of cases without any regexp tweaking.
   * `name_regepx` is useful for series which are written in more than one way
 * If specifying name_regexp(s) make sure that these match only to the given series
 * Pay attention to the ''indentation'' here

'''Example:'''

{{{
series:
  - some series:
      name_regexp: ^some.series
      ep_regexp: (\d\d)-(\d\d\d)  # must return TWO groups, both being numeric values
      id_regexp: (\d\d\d)         # can return any number of groups
  - another series
  - third series
}}}

All above regexps also accept multiple regular expressions in list form.

For example if `some series` appears in two different naming conventions, you can:

{{{
- some series:
    name_regexp:
      - ^some.series
      - ^some.srs
}}}

=== Episode numbering matching ===

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