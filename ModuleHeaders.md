= Headers =

Allows editing request headers. This will affect everything that uses urllib2 to do requests, this should include most of the modules.
To use feeds that require cookies, headers are required! You must find the cookie for the site, and grab UID and pass from it.

== Example: ==

Set cookie:

{{{
headers:
  Cookie: "uid=3945; pass=f8bae52ca325b14ef2523fabc"
}}}

== How to find UID / pass ==

 * IE users will find their cookies in %!UserProfile%\Cookies
 * Firefox users will find their cookies in Tools -> Options -> Privacy -> Cookies -> Show Cookies. (or the addon Export cookies may be used)
 * Opera users will find their cookies in Tools -> Advanced -> Cookies
