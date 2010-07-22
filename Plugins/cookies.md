= Cookies =

Loads cookies from a file. Supports Firefox3, mozilla, and lwp cookie files.

=== Example ===

{{{
cookies: ~/.flexget/cookies.sqlite
}}}

== Types ==

This plugin will attempt to determine what type of cookies file you are using based on the extension.
||'''Extensions'''||'''Type'''||
||.txt||mozilla||
||.lwp||lwp||
||all others||firefox3||

If you would like to override this behavior, a cookie type can be specified manually like this:

{{{
cookies:
  file: /path/to/cookies.foo
  type: mozilla
}}}

'''Notes:'''
 - You cannot read cookies from running Firefox! Shutdown browsed and make a copy from `cookies.sqlite` to somewhere (ie. `~/.flexget`)
 - Support for mozilla and lwp cookies was added in r1325