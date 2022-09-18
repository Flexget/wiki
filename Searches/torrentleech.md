---
title: torrentleech
description: 
published: true
date: 2022-09-18T05:19:01.950Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:59.329Z
---

# Torrentleech
This search plugin will get results from [http://torrentleech.org](/http://torrentleech.org)

## Configuration
Configuration requires rss_key, username, and password: (RSS key will be found in your TL account preferences while username and password are your usual TL login credentials. Omit the URL component (http://rss.torrentleech.org/) including the trailing slash.)
```
torrentleech: 
  rss_key: 8450c277413e1befe8bb
  username: cinefilo1979
  password: 05f9b0f6%
```
If you would like to define a custom category, you can use the following option:
 category::
 Can be one of the following: \\
      all, Cam, TS, R5, DVDRip, DVDR, HD, BDRip, Boxsets, Documentaries \\\\
 You can also specify the category number directly from Torrentleech if it is not listed above. \\
 
Example:
```
torrentleech: 
  rss_key: 8450c277413e1befe8bb
  username: cinefilo1979
  password: 05f9b0f6%
  category: 4K
```