= Headers =

Allows editing request headers. This will affect most of the modules (everything that uses urllib2). To use feeds that require login, setting cookie is usually required. You will need to extract the cookie for site and grab details from it (usually uid, pass).

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
