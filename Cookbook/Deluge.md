# Flexget & Deluge on Ubuntu

The following is a comprehensive guide on how to setup an ubuntu box as a seedbox with flexget and deluge. By working through this guide, you can have an automated torrenting setup with the following features:

* Automatically download episodes of tv shows you have watchlisted on your trakt.tv account.
* Automatically download movies you have watchlisted on your imdb account.
* Use deluge as the client for automatically downloading matched torrents.
* Use multiple rss feeds as inputs for each task for redundancy.
* Receive push notifications via pushbullet for each torrent added to deluge.
* Movies and tv shows are downloaded in to seperate folders.
* Torrents that contain rar files will be automatically extracted.
* Use a custom download manager for downloading completed/extracted files from the seedbox to your local computer. `(requires a linux computer on your local network)`
* Download manager automatically deletes successfully downloaded files/folders from the seedbox.
* Download manager does not touch the original torrent content so that you can seed for as long as you like.
* Download manager uses secure SSL connections to the seedbox for protecting privacy.

<div class="alert alert-info" role="alert">

**You can access the full tutorial by [clicking here](https://djnitehawk.com/flexget.htm)**
</div>