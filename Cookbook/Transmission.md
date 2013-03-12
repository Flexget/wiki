[[BR]]
this is the setup i have on my ubuntu VPS that acts as a seedbox but you can adapt it to suit your needs easily.

it is a complete A-Z guide/cookbook for setting up flexget with transmission that has the following features:
----
- auto download movie torrents matching your imdb watchlists:
 - remember downloaded movies and never download the same movie twice.
 - 2 different watchlists: 
  - main imdb watchlist for downloading torrents that are dvdrips or bdrips with a resolution lower than 720p
  - hd watchlist for downloading torrents that are bdrips with a resolution of exactly 720p

- send a push notification to your mobile device via boxcar when a new torrent is added to transmission

- auto download tv torrents that match your thetvdb favorites list. and remember already downloaded episodes so that the same episode wont get downloaded twice.

- ability to exclude tv torrents from release groups that you dont like.

- download movie and tv torrents into 2 separate folders.

- ignore propers and repacks for both tv and movies.

- a custom cron script to run flexget periodically that has the following features:
 - run every 30 mins
 - check if flexget is still running from the previous cron cos sometimes flexget just hangs and subsequent cron runs fail.
 - check for an orphaned config lock file cos if there's an orphaned config lock file, flexget wont run.
 - check if transmission is running and inform you via push notification if it's crashed.

if/when you get a notification saying that transmission is not running, you have to do the following to make sure you wont miss any torrents:
{{{
1.) start the transmission daemon manually or restart the machine.
2.) edit your config.yml and find and replace "all_entries: no" with "all_entries: yes"
3.) run flexget once manually
4.) undo the change u did above to your config.yml
}}}

- a custom post-processing script for transmission that will run when each torrent is complete:
 - leaves the original files alone and extracts rars to a final folder so u can keep seeding the original content.
 - if the content is not rar'ed, makes a copy at the final folder so u can keep seeding the original content.
 - deletes sample video files at the final folder.
 - sends a push notification if extracting rars fails.
 - verify and restart the torrent once, if extracting rars fails.
 - logs unrar'ed, copied and error'ed torrent names to a text file.
 - 
----
special requirements:

- rss feed urls from either private or public trackers that support passwordless downloading. (i use IPTorrents in this guide)
- imdb account (https://secure.imdb.com/register-imdb/form-v2)
- thetvdb account (http://thetvdb.com/?tab=register)
- boxcar provider account (http://boxcar.io/site/providers)
- an apple device to install boxcar app on (mac/ipod touch/iphone/ipad)
- this cookbook is ubuntu/linux based but you can adapt it to your non linux needs if you know what you are doing :-)
----
