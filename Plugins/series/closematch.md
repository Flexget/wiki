= How to deal with similarly named series =

=== Case: Other series confuses the one I want ===

You want to add series "foobar" into your configuration but there's also spinoff series called "foobar us" which you are not interested. Simplest way to prevent !FlexGet getting confused about the "foobar s02e01" and "foobar us s01e01" is to specify [wiki:Plugins/series/exact exact] option.

But as exact mode will stop matching when titles like "foobar.sub.title.s01e01" (rare) appear you might want to use [wiki:Plugins/series/regexps name_regexp].

'''Example'''

{{{
series:
  - foobar:
      name_regexp: ^foobar(?!.us)
}}}

This will use name detection regexp that will match to foobar but not when it's followed by us.

=== Case: Series written in different ways ===

Series name appears in multiple different ways. For example series "foobar" is sometimes spelled as "foobar 2005". Do not under any circumstances list this series twice in the configuration, it will confuse episode tracking (advancement) and you will get really weird results, if any.

Instead list the series just once and use the form is more common, note that this name is what !FlexGet uses everywhere including [wiki:Plugins/tmdb_lookup tmdb_lookup] etc. And then use series plugin [wiki:Plugins/series/regexps name_regexp] option.

'''Example'''

{{{
series:
  - foobar:
      name_regexp: ^foobar(.2005)?
}}}

The regexp in question will match "foobar" and "foobar 2005"
