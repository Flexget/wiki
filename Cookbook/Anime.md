{{{To the author:}}} Does series plugin not work for you?

For a long time, I would organize my anime collection as I would acquire it.  Each series would go directly into it's own folder.  And then my HDD died, presumably due to all the stress of constantly serving files.

So now, I have a smaller HDD that I use to simply dump files into.  Once the series is complete, I transfer it all over to storage, which remains blissfully unstressed.  My torrent client is set up to watch the Temp directory where the torrent files are downloaded.  I'm not using Deluge in Windows 7 since I've had it crash on me multiple times.  From R:\Temp, the client saves all of the files into a Videos folder.  Viewing this folder in Windows Explorer works out pretty well, when sorted by timestamp.

{{{
presets:
    anime:
        download: R:\Temp
feeds:
    Nyaa Torrents:
        rss: http://www.nyaa.eu/?page=rss&cats=1_37&filter=2
        preset: anime
        regexp:
            accept:
                - '\[Commie\].Rinne.*mkv'
                - '\[WhyNot\].Koi.to.Senkyo.to.Chocolate.*mkv'
                - '\[Taka\].Natsuyuki.Rendezvous.*720.*mkv'
                - '\[UTWoots\].Sword.Art.Online.*mkv'
                - '\[UTW\].*Accel.*World.*mkv'
                - '\[Commie\].*Hyouka.*mkv'
                - '\[gg.*\].*Jormungand.*mkv'
                - '\[Commie\].*Space.Brothers.*mkv'
                - '\[ray=out\].*Before.*Green.*Gables.*HD.*mkv'
    Doki Anime Index:
        html: 
            url: http://tracker.anime-index.org/index.php?page=torrents&search=doki&category=5&active=1
            title_from: url
        preset: anime
        regexp:
            accept:
                - '\[Doki\].*Junrui.Wa.Suitai.Shimashita.*720.*mkv.torrent'
                - '\[Doki-Chihiro\].Kokoro.Connect.*720.*mkv.torrent'
                - '\[Doki\].Tari.Tari.*720.*mkv.torrent'
}}}

Since Tokyo Toshokan has been kind of flaky lately, and Doki doesn't show up on Nyaa, I'm using their own tracker.  The tracker doesn't support RSS yet, so I'm ripping the torrent links from it directly.