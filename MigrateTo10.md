= Migrating from 0.9 to 1.0 =

''Under work''

== New dependency ==

!FlexGet 1.0 requires SQLAlchemy 0.5 or newer. Install it from your distribution repository or from http://sqlalchemy.org

Another easy way is to use easy_install (comes with setup tools).

{{{
easy_install sqlalchemy
}}}

== Session migration ==

!FlexGet 1.0 imports some information from 0.9 but not all. At the time of writing this only already downloaded content is imported.

== Deprecated modules ==

Some modules have been replaced with new ones.

=== Patterns, Ignore, Accept ===

These modules have been removed. You'll need to convert these to use new [wiki:FilterRegexp regexp] module. Luckily this is not hard to do since syntax is almost identical.

{{{
patterns:
  - foo
  - bar
ignore:
  - xxx
  - yyy
}}}

Converts into:

{{{
regexp:
  accept:
    - foo
    - bar
  reject:
    - xxx
    - yyy
  rest: filter
}}}

Unfortunately a bit more complex, but this is more explicit of what it does and covers a lot more situations.

=== Cookies ===

''TODO''