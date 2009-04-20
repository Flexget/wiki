= Better alternative =

You may wish to check [wiki:ModuleHeaders headers] module, in my opinion it is currently easier way to set a cookie.

= Cookies =

It is possible that this module will be '''[wiki:ToBeRemoved deprecated]'''.

Adds cookie to all requests (rss, resolvers, download). Anything that uses urllib2 to be exact.

Configuration:

{{{
cookies:
  type: mozilla
  file: /path/to/cookie
}}}

Possible cookie types are: mozilla, ~~msie, lpw~~

'''Note:''' Only mozilla cookies are supported right now, there is a ticket open for this issue (#38).

== Important ==

!FireFox3 doesn't store cookies anymore in a {{{cookies.txt}}} so they must be exported by using utility (example: https://addons.mozilla.org/en-US/firefox/addon/8154).

Mozilla cookies-file '''must begin''' with following lines or it doesn't load. Usually this is the case, but not always.

{{{
# HTTP Cookie File
# http://www.netscape.com/newsref/std/cookie_spec.html
# This is a generated file!  Do not edit.
# To delete cookies, use the Cookie Manager.
}}}

If you edit the file note that values '''must be separated with tab''', not by spaces.

These inconveniences will be addressed in the future ...