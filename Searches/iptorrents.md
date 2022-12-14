---
title: iptorrents
description: 
published: true
date: 2022-12-14T19:06:09.018Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:17:57.391Z
---

# IPTorrents
> This plugin is part of [search](/Plugins/Searches) plugin system.
{.is-success}

This search plugin will get results from [http://iptorrents.com](http://iptorrents.com).

## Configuration

### Required Configuration
`rss_key`, `uid`, and `password` strings are required:
```
iptorrents: 
  rss_key: xxxxx
  uid: xxxxx
  password: xxxxx
```

### Optional Configuration

#### Category

If you would like to search within a custom category, you can use the `category` list option:
```
iptorrents: 
  rss_key: xxxxx
  uid: xxxxx
  password: xxxxx
  category:
    - all
```

 This list can contain one or more of the following:
 ```
 all
 Movie-3D
 Movie-480p
 Movie-BD-R
 Movie-BD-Rip
 Movie-DVD-R
 Movie-HD-Bluray
 Movie-Kids
 Movie-MP4
 Movie-Non-English
 Movie-Packs
 Movie-XviD
 TV-all
 TV-Sports
 TV-480p
 TV-MP4
 TV-Non-English
 TV-Packs
 TV-Packs-Non-English
 TV-SD-x264
 TV-Web-DL
 TV-x264
 TV-XVID
 ```
 
***Note**: these categories may change over time, it is recommended to check IPTorrents for up-to-date category names.*

You can also specify the category number directly from IPTorrents if it is not listed above:
```
iptorrents: 
  rss_key: xxxxx
  uid: xxxxx
  password: xxxxx
  category: 
    - Movie-HD-Bluray
    - Movie-MP4
    - 22
```

#### Free

If you would only like to search for freeleach content, use the `free` boolean option:

```
iptorrents: 
  rss_key: xxxxx
  uid: xxxxx
  password: xxxxx
  free: True
```

## Location of Required Configuration Values

### `rss_key`

`rss_key` can be found under "Passkey" in the IPTorrents account page:

<img src="http://i.imgur.com/XinVDly.jpg">

### `uid` and `password`

Both `uid` and `password` are located inside the IPTorrents cookie.

To view this in the Chrome browser, first navigate to [http://iptorrents.com](/http://iptorrents.com) and login.

Open Chrome options -> `More tools` -> `Developer tools` (Or press Ctrl+Shift+I):

<img src="http://i.imgur.com/qzlrjA9.jpg">  

Choose `Applications` (n.b. not `Resources`) in the newly-opened tab:

<img src="http://i.imgur.com/jNFu4Cq.jpg">  

Navigate to `IPTorrents` under `Cookies`. `uid` and `password` are listed there:

<img src="http://i.imgur.com/45WW0Ok.jpg">
