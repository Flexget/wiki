# IPTorrents
This search plugin will get results from [http://iptorrents.com](http://iptorrents.com)

## Configuration
Configuration requires rss_key, uid, and pass (see below):
```
iptorrents: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  uid: xxxxx
  password: xxxxxxxxx
```
If you would like to define a custom category, you can use the following option:
 category::
 Can be one of the following: \\
      all, Movie-3D, Movie-480p,Movie-BD-R, Movie-BD-Rip, Movie-DVD-R, Movie-HD-Bluray, Movie-Kids, Movie-MP4, Movie-Non-English, Movie-Packs, Movie-XviD, TV-all, TV-Sports, TV-480p, TV-MP4, TV-Non-English, TV-Packs, TV-Packs-Non-English, TV-SD-x264, TV-Web-DL, TV-x264, TV-XVID \\\\
 You can also specify the category number directly from iptorrents if it is not listed above. \\
 
Example:
```
iptorrents: 
  rss_key: xxxxxxxxxxxxxxxxxxxx
  uid: xxxxxx
  password: xxxxxx
  category: 
    - Movie-HD-Bluray
    - Movie-MP4
    - 22
```

== Location of rss_key,uid, password== 

rss_key can be found under "Passkey" in the IPTorrents account page:  

<img src="http://i.imgur.com/XinVDly.jpg">

  

Both the uid and the password are located inside the IPtorrent cookie. To view it in the Chrome browser, first navigate to [http://iptorrents.com](/http://iptorrents.com) and login.
Open Chrome options -> More Tools -> Developer Tools (Or press Ctrl+Shift+I)  

<img src="http://i.imgur.com/qzlrjA9.jpg">  

Choose 'Resources' in the newly open tab  

<img src="http://i.imgur.com/jNFu4Cq.jpg">  

Navigate to IPTorrens under Cookies, uid and password are listed there.
  

<img src="http://i.imgur.com/45WW0Ok.jpg">

  
