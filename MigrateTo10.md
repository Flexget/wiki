= Migrating from 0.9 to 1.0 (alpha) =

'''Notes'''

 * Instructions under work ..
 * 1.0 is still not ready, but begins to be somewhat usable

== New dependencies ==

'''Python 2.5''' - older versions will no longer be supported.[[BR]]
'''Easy_install'''

== Install ==

Currently only way to install is to checkout from [wiki:Subversion subversion].

After checkout you must initialize environment by running:

{{{
python bootstrap.py
}}}

Note that flexGet executable has also been relocated, it is now in:

{{{
bin/flexget
}}}

Copy your old session and configuration file to new install.

'''Do not execute your configuration without --test until --check passes.'''

== Session migration ==

!FlexGet 1.0 imports some information from 0.9 but not all. At the time of writing this only already downloaded content is imported.

== Deprecated modules ==

Some modules have been replaced with new ones.

=== Patterns, Ignore and Accept ===

These modules have been removed. You'll need to convert these to use new [wiki:FilterRegexp regexp] module. Luckily this is not hard to do since syntax is almost identical.

'''Patterns:'''

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

'''Ignore:'''

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

=== Imdb ===

{{{filter_invalid}}} has been changed into {{{reject_invalid}}} since filter operation has been removed.

== Series ==

Timeframe syntax has been changed, see [http://flexget.com/wiki/FilterSeries10#Timeframe here].

=== Cookies ===

New plugin, see [wiki:ModuleCookies10 cookies]

=== Downloading complete feeds ===

In 0.9 feeds were implicitly downloaded completely without any accept. Ie

{{{
rss: <url>
download: <path>
}}}

Would have downloaded everything, this has been changed in 1.0 for various reasons.

{{{
rss: <url>
accept_all: true
download: <path>
}}}

== First run ==

Your first run with 1.0 should execute all feeds, so use {{{--now}}} if necessary to force feeds with [wiki:ModuleInterval interval] to execute.