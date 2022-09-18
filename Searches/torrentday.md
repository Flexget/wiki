---
title: torrentday
description: 
published: true
date: 2022-09-18T05:18:58.058Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:55.430Z
---

# Torrentday
This search plugin will get results from [https://torrentday.com](https://torrentday.com)

## Configuration
Configuration requires the 3 cookies from an active login session. You also need rss_key (found in your TD account preferences page). 
```
torrentday:
  uid: xxxxxxxx (required) NOT YOUR LOGIN. find this in your browser's cookies
  passkey: xxxx (required) NOT YOUR PASSWORD. see previous
  cfduid: xxxxx (required) AGAIN IN THE COOKIES
  rss_key: xxxx (required) get this from your profile page
  category: xxx
```
category, Can be *one* of the following: 
- *for movies:* mov480p, movHD, movBD, movDVD, movMP4, movNonEnglish, movPACKS, movSDx264, movX265, movXVID
- *for tv:* tv480p, tvBRD, tvDVD, tvDVDrip, tvMOBILE, tvPACKS, tvSDx264, tvHDx264, tvX265, tvXVID

 You can also specify the category number directly from Torrentday if it is not listed above. Excluding category will search all.
 
 ## How to get your cookies
 ### chrome
 - Go to TD > Login if you haven't already
 - Right click then left click *Inspect Elements* (or hit *Ctrl+Shift+I*)
 - Go to *Applications tab* across the top, then *Cookies* on the left
   - expand it if you have to and click on *td*
 - For each of the 3 cookies, right click on the value (redacted from the screenshot), copy
 - Paste into your flexget config
 
 <img src=http://i68.tinypic.com/2qvqb1g.png>

### FireFox
- From the Tools menu, select *Preferences*
- Along the top, click the *Privacy* tab
- Click *remove individual cookies*
- Search for *torrentday*
- copy the *Content* for each of the 3 cookies (redacted from the screenshot)
- Paste into your flexget config
 
<img src=http://i63.tinypic.com/2e6cufr.png>

### Reference
https://kb.iu.edu/d/ajfi
( Includes steps for Safari and IE )
## Example Config
```
tasks:
  moviesTOdiscoverFROMtd:
    discover:
      what:
        - movie_list: moviesTOget
      from:
        - torrentday:
            uid: '123456'
            cfduid: 1234567890abcdef1234567890abcdef1234567890abcd
            passkey: 1234567890abcdef1234567890abcdef
            rss_key: 1234567890abcdef1234567890abcdef
            category: movHD
    list_match:
      from:
        - movie_list: moviesTOget
    list_remove:
      - movie_list: moviesTOget
```
