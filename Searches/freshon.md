= Freshon =
This search plugin will get results from [http://FreshOn.tv]

== Configuration ==
Configuration requires username, and password:
{{{
freshon: 
  username: xxxxxx
  password: xxxxxx
}}}
If you would like to define a custom category, you can use the following option:
 category::
 Can be one of the following (Specifies specific tabs on Freshon): \\
      all, webdl, hd \\\\

If you would like only 100% or 50% freeleech, you can use the following option:
 freeleech::
 Can be one of the following: \\
      all, free, half \\\\
 
Example:
{{{
freshon: 
  username: xxxxxx
  password: xxxxxx
  category: hd
  freeleech: half
}}}

Supports pagination, maximum pages is 10. Number of items per page is set in the user CP at site; can only be set if you are above a certain user level. Maximum items per page is 100 meaning a total of 1000 search results maximum.