= IPTorrents =
This search plugin will get results from [http://iptorrents.com]

== Configuration ==
Configuration requires rss_key, uid, and pass (uid and pass are found in the cookies):
{{{
iptorrents: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  uid: xxxxx
  password: xxxxxxxxx
}}}
If you would like to define a custom category, you can use the following option:
 category::
 Can be one of the following: \\
      all, Movie-3D, Movie-480p,Movie-BD-R, Movie-BD-Rip, Movie-DVD-R, Movie-HD-Bluray, Movie-Kids, Movie-MP4, Movie-Non-English, Movie-Packs, Movie-XviD, TV-all, TV-Sports, TV-480p, TV-MP4, TV-Non-English, TV-Packs, TV-Packs-Non-English, TV-SD-x264, TV-Web-DL, TV-x264, TV-XVID \\\\
 You can also specify the category number directly from iptorrents if it is not listed above. \\
 
Example:
{{{
iptorrents: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  uid: xxxxxx
  password: xxxxxx
  category: 
    - Movie-HD-Bluray
    - Movie-MP4
    - 22
}}}