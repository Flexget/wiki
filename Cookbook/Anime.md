---
title: Anime
description: 
published: true
date: 2022-09-18T04:54:58.717Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:56.146Z
---

For a long time, I would organize my anime collection as I would acquire it.  Each series would go directly into it's own folder.  And then my HDD died, presumably due to all the stress of constantly serving files.

So now, I have a smaller HDD that I use to simply dump files into.  Once the series is complete, I transfer it all over to storage, which remains blissfully unstressed.  My torrent client is set up to watch the Temp directory where the torrent files are downloaded.  I'm not using Deluge in Windows 7 since I've had it crash on me multiple times.  From R:\Temp, the client saves all of the files into a Videos folder.  Viewing this folder in Windows Explorer works out pretty well, when sorted by timestamp.

```
templates:
    global:
        download: R:\Temp
        notifymyandroid:
            apikey: YOUR_API_KEY_HERE
    anime:
        series:
            - Rinne no Lagrange: {from_group: Commie}
            - Koi to Senkyo to Chocolate: {from_group: WhyNot}
            - Natsuyuki Rendezvous: {from_group: Taka, quality: 720p}
            - Sword Art Online: {from_group: UTWoots}
            - Accel World: {from_group: UTW}
            - Space Brothers: {from_group: Commie}
            - Before Green Gables: {from_group: ray=out}
            - Hyouka: {from_group: Commie}
            - Binbougami ga: {from_group: gg}
            - Eureka Seven AO: {from_group: gg}
            - Junrui Wa Suitai Shimashita: {from_group: Doki, quality: 720p}
            - Kokoro Connect: {from_group: Doki-Chihiro}
            - Tari Tari: {from_group: Doki}
            - Yuru Yuri S2: {from_group: FFF}
feeds:
    Anime:
        inputs:
            #- rss: http://tokyotosho.info/rss.php?filter=1
            - rss: http://www.nyaa.eu/?page=rss&cats=1_37&filter=2
            - html: 
                url: http://tracker.anime-index.org/index.php?page=torrents&search=doki&category=5&active=1
                title_from: url
        template: anime
```

Since Tokyo Toshokan has been kind of flaky lately, and Doki doesn't show up on Nyaa, I'm using their own tracker.  The tracker doesn't support RSS yet, so I'm ripping the torrent links from it directly.