= Cookies =

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

!FireFox3 doesn't store cookies anymore in a {{{cookies.txt}}} so you need to export this by using some sort of utility. Take a look at https://addons.mozilla.org/en-US/firefox/addon/8154.

Mozilla cookies-file '''must begin'' with following lines or it doesn't load. Usually this is the case, but not always.

{{{
# HTTP Cookie File
# http://www.netscape.com/newsref/std/cookie_spec.html
# This is a generated file!  Do not edit.
# To delete cookies, use the Cookie Manager.
}}}

Cookie values in a single line '''must be separated with tab''', not by spaces.

These inconveniences will be addressed in ticket #38, blame pythons cookielib ... 