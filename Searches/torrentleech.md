= Torrentleech =
This search plugin will get results from [http://torrentleech.org]

== Configuration ==
Configuration requires rss_key, username, and password:
{{{
torrentleech: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  username: xxxxxx
  password: xxxxxx
}}}
If you would like to define a custom category, you can use the following options:
 category::
 Can be one of the following: \\
      all, Cam, TS, R5, DVDRip, DVDR, HD, BDRip, Boxsets, Documentaries \\

 You can also specify the category number directly from Torrentleech if it is not listed above. \\
 
Example:
{{{
torrentleech: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  username: xxxxxx
  password: xxxxxx
  category: HD
}}}