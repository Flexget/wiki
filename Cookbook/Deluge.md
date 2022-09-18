---
title: Deluge
description: 
published: true
date: 2022-09-18T04:55:13.762Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:11.145Z
---

# Flexget & Deluge on Ubuntu

The following is a comprehensive guide on how to setup an ubuntu seedbox/vps with flexget and deluge. By working through this guide, you can have an automated torrenting setup with the following features:

* Automatically download new episodes of tv shows you have watchlisted on your trakt.tv account.
* Automatically download movies you have watchlisted on your imdb account.
* Use deluge as the client for automatically downloading matched torrents.
* Use multiple rss feeds as inputs for each task for redundancy.
* Receive push notifications via pushbullet for each torrent added to deluge.
* TV shows are downloaded in `720p x264 hdtv or webdl or webrip` quality.
* Movies are downloaded in `720p or 1080p x264 bdrip` quality.
* Movies and tv shows are downloaded into seperate folders.
* Torrents that contain rar files will be automatically extracted.
* Use a custom download manager for downloading completed/extracted files from the seedbox to your local computer. `(requires linux)`
* Download manager automatically deletes successfully downloaded files/folders from the seedbox.
* Download manager does not touch the original torrent content so that you can seed for as long as you like.
* Download manager uses secure SSL connections to the seedbox for protecting privacy.

> **You can access the full tutorial by [clicking here](https://djnitehawk.com/flexget.htm)**
{.is-info}

### PDF Download
You can download a PDF version of the tutorial from the following google drive link:

```
https://drive.google.com/open?id=0BzU4nr8FNKaKeGpPTmdrY3lzbUE
```