== Identified by ==

Specify how episode number is detected.

'''Example:'''

{{{
series:
  - pioneer one:
      identified_by: ep
}}}

Possible values: `ep`, `id`, `auto`

Default value is `auto` which uses episode history to detect what to use. In absence of reliable history both `ep` and `id` format are accepted.

=== What is ep ===

Series which are identified by season, episode. 

'''Some Examples:'''

 * S01E02
 * 01x02

=== What is id ===

Series that are identified by number or date.

'''Some Examples:'''

 * 01
 * 10.10.2010

=== Custom matching ===

!FlexGet identifies almost everything by default, but sometimes it may be necessary to customize matching. This can be achieved via [wiki:Plugins/series/regexps ep_regexp and id_regexp].