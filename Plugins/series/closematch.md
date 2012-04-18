= How to deal with similarly named series =
There are a few ways to deal with this problem, but this simplest is this:

=== Use parentheses to specify an optional part of the name ===

You want to add series "foobar" into your configuration, which is also sometimes released as "foobar uk". Just putting "foobar" in your config will match both of these fine. But say there's also spinoff series called "foobar us" which you are not interested. Simplest way to prevent !FlexGet getting confused about the "foobar s02e01" and "foobar us s01e01" is to put the "uk" in parentheses, i.e. "foobar (uk)". This will cause !FlexGet to allow both the "foobar s02e01" and "foobar uk s02e01" forms, but not "foobar us s02e01".

'''Example'''
{{{
series:
  - foobar (uk)
}}}
--------------
'''{{{NOTE:}}}''' The above parentheses method can solve most of the issues with similarly named series. The following methods were used before the above technique was developed, and should not be needed any more in the majority of cases.
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