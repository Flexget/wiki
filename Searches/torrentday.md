# Torrentday
This search plugin will get results from [https://torrentday.com](/https://torrentday.com)

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