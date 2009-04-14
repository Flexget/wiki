= Migrating from 0.9 to 1.0 =

'''Notes'''

 * Instructions under work ..
 * 1.0 is still light years away from being released ...

== New dependencies ==

'''Python 2.5''' - older versions will no longer be supported.[[BR]]
'''SQLAlchemy 0.5''' or newer. Install it from your distribution repository or from http://sqlalchemy.org

Another easy way is to use easy_install (comes with setup tools).

{{{
easy_install sqlalchemy
}}}

== Session migration ==

!FlexGet 1.0 imports some information from 0.9 but not all. At the time of writing this only already downloaded content is imported.

== Deprecated modules ==

Some modules have been replaced with new ones.

=== Patterns, Ignore and Accept ===

These modules have been removed. You'll need to convert these to use new [wiki:FilterRegexp regexp] module. Luckily this is not hard to do since syntax is almost identical.

{{{
patterns:
  - foo
  - bar
}}}

Converts into:

{{{
regexp:
  accept:
    - foo
    - bar
}}}

{{{
ignore:
  - xxx
  - yyy
}}}

Converts into:

{{{
regexp:
  reject:
    - xxx
    - yyy
}}}

Combination of both would be:

{{{
regexp:
  accept:
    - foo
    - bar
  reject:
    - xxx
    - yyy
}}}

Unfortunately a bit more complex, but this is more explicit in !FlexGet terminology what it does and covers a lot more situations.

=== Regexp ===

Filtering system has been simplified a bit in 1.0, this requires few changes in regexp configuration. Remove all {{{rest: filter}}} lines.

=== Cookies ===

''TODO''

== First run ==

Your first run with 1.0 should execute all feeds, so use {{{--now}}} if necessary to force feeds with [wiki:ModuleInterval interval] to execute.