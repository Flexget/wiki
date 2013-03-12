this is a complete configuration setup for flexget with transmission that has the following features:
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
----
special requirements:

- imdb account (https://secure.imdb.com/register-imdb/form-v2)
- thetvdb account (http://thetvdb.com/?tab=register)
- boxcar provider account (http://boxcar.io/site/providers)
- an apple device to install boxcar app on (mac/ipod touch/iphone/ipad)
- this cookbook is ubuntu/linux based but you can adapt it to your non linux needs if you know what you are doing :-)
----
