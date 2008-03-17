= Cookies =

Adds cookie to all requests (rss, resolvers, download). Anything that uses urllib2 to be exact.

Configuration:

{{{
cookies:
  type: mozilla
  file: /path/to/cookie
}}}

Possible cookie types are: mozilla, msie, lpw

== Note ==

Mozilla cookies-file must begin with following lines or it doesn't load. Usually this is the case, but not always.

{{{
# HTTP Cookie File
# http://www.netscape.com/newsref/std/cookie_spec.html
# This is a generated file!  Do not edit.
# To delete cookies, use the Cookie Manager.
}}}
