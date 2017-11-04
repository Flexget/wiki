## A Complete Transmission Recipe
**`ATTENTION:`** This recipe is for an older version of FlexGet and may not be valid anymore. An updated guide with similar features has been posted for deluge [here](/Cookbook/Deluge). 

this is a user contributed recipe. it is the setup i have on my ubuntu VPS that acts as a seedbox but you can adapt it to suit your needs easily.  
it is a complete A-Z recipe for setting up flexget with transmission with a whole bunch of features that makes torrenting a lot less tedious.
----
**FEATURES:**

- auto download movie torrents matching your imdb watchlists:
  - remember downloaded movies and never download the same movie twice.
  - 2 different watchlists: 
    - main imdb watchlist for downloading torrents that are 'dvdrips' or 'bdrips' with a resolution lower than '720p'
    - hd watchlist for downloading torrents that are 'bdrips' with a resolution of exactly '720p'

- auto download tv torrents that match your thetvdb favorites list.
  - remember already downloaded episodes so that the same episode wont get downloaded twice.
  - only download torrents that are 'hdtv' source and resolution is below '720p'
  - ability to exclude tv torrents from release groups that you dont like.

- download movie and tv torrents into 2 separate folders.

- send a push notification to your mobile device via boxcar when a new torrent is added to transmission

- ignore propers and repacks for both tv and movies.

- only downloads new items from rss feeds.

- a custom cron script to run flexget periodically that has the following features:
  - run every 30 mins
  - check if flexget is still running from the previous cron cos sometimes flexget just hangs and subsequent cron runs fail.
  - check for an orphaned config lock file cos if there's an orphaned config lock file, flexget wont run.
  - check if transmission is running and inform you via push notification if it's crashed.

- a custom post-processing script for transmission that will run when each torrent is complete:
  - leaves the original files alone and extracts rars to a final folder so u can keep seeding the original content.
  - if the content is not rar'ed, makes a copy at the final folder so u can keep seeding the original content.
  - deletes sample video files at the final folder.
  - sends a push notification if extracting rars fails.
  - verify and restart the torrent once, if extracting rars fails.
  - logs unrar'ed, copied and error'ed torrent names to a text file.
  - skip postprocessing on any torrents that are added to a folder called "RATIO" which you can place manually added torrents in for building up your ratio, and wont need to download to your local machine.

- a custom download manager script you can use to download files to your local computer from your VPS/seedbox
  - uses aria2 download manager with 10 simultaneous connections
  - resumes broken downloads
  - automatically times out and retries stalled downloads
  - uses SSL with a self signed certificate so your ISP cant spy on what you are downloading.
  - can limit the bandwidth used for downloading files
  - removes the successfully downloaded files from your VPS/seedbox
  - no need to SSH into your VPS/SB as the file listing/transfers/deletion is done via lighttpd webserver and php.
  - ability to display a list of files that are on the final folder at your VPS/SB without actually downloading them.
  - logs failures to a text file.

----

**SPECIAL REQUIREMENTS:**

- rss feed urls from either private or public trackers that support passwordless downloading. (i use IPTorrents in this guide)
- imdb account (https://secure.imdb.com/register-imdb/form-v2)
- thetvdb account (http://thetvdb.com/?tab=register)
- boxcar provider account (http://boxcar.io/site/providers)
- an apple device to install boxcar app on (mac/ipod touch/iphone/ipad)
- everything is tested and works perfectly on ubuntu 12.04 and your results may vary with other versions.

----

**GET THE 3RD PARTY STUFF READY:**

**IMDB:**  

```
log into your imdb account and add a few movies to your default "Watchlist".
then create a new watchlist called "HDWatchlist" and add a couple of movies to that too.
then open up that HDWatchlist and have a look at the url. it would be in the form of: http://www.imdb.com/list/XXXXX/
write down or make a note of the string of characters that's at the XXXXX part. we need this ID as flexget doesnt support additional watchlists by their name.
```

**THETVDB:**

```
log into the site and visit the following url: http://thetvdb.com/?tab=userinfo
make note of the "Account Identifier". also dont forget to add a few tv series to your favorites while you are there.
```

**BOXCAR:**

```
install the boxcar app on your idevice.
log into your boxcar account and create a new provider at http://boxcar.io/site/providers
open up the newly created provider and make note of the "Your API key is:" field.
```

----

**PREPARE TRANSMISSION**

ssh or log in to your ubuntu box and run the following commands one after the other:

**note:** replace "djnitehawk" with your username  

```
cd ~/
sudo apt-get install python-software-properties
sudo add-apt-repository ppa:transmissionbt/ppa
sudo apt-get update
sudo apt-get install transmission-daemon
sudo useradd -g transmission-daemon djnitehawk
echo "" > prep-dirs.sh
chmod +x prep-dirs.sh
nano prep-dirs.sh
```

**troubleshooting:** if the "useradd" command above says the group doesn't exist, restart the machine first and try "sudo adduser djnitehawk debian-transmission"

then copy and paste the following text into nano:

**note:** replace "djnitehawk" with your username

``` /bin/bash
mkdir /home/djnitehawk/Downloads
echo "dont delete this dir" > /home/djnitehawk/Downloads/.lock
mkdir /home/djnitehawk/Downloads/MOVIES
echo "dont delete this dir" > /home/djnitehawk/Downloads/MOVIES/.lock
mkdir /home/djnitehawk/Downloads/OTHER
echo "dont delete this dir" > /home/djnitehawk/Downloads/OTHER/.lock
mkdir /home/djnitehawk/Downloads/STORAGE
echo "dont delete this dir" > /home/djnitehawk/Downloads/STORAGE/.lock
mkdir /home/djnitehawk/Downloads/TV-SHOWS
echo "dont delete this dir" > /home/djnitehawk/Downloads/TV-SHOWS/.lock

mkdir /home/djnitehawk/Ready
echo "dont delete this dir" > /home/djnitehawk/Ready/.lock
mkdir /home/djnitehawk/Ready/Completed
echo "dont delete this dir" > /home/djnitehawk/Ready/Completed/.lock
mkdir /home/djnitehawk/Ready/MEDIA
echo "dont delete this dir" > /home/djnitehawk/Ready/MEDIA/.lock
mkdir /home/djnitehawk/Ready/MEDIA/MOVIES
echo "dont delete this dir" > /home/djnitehawk/Ready/MEDIA/MOVIES/.lock
mkdir /home/djnitehawk/Ready/MEDIA/STORAGE
echo "dont delete this dir" > /home/djnitehawk/Ready/MEDIA/STORAGE/.lock
mkdir /home/djnitehawk/Ready/MEDIA/TV-SHOWS
echo "dont delete this dir" > /home/djnitehawk/Ready/MEDIA/TV-SHOWS/.lock

mkdir /home/djnitehawk/Downloads/RATIO
echo "dont delete this dir" > /home/djnitehawk/Downloads/RATIO/.lock

chown -R djnitehawk:debian-transmission /home/djnitehawk/Downloads
chown -R djnitehawk:debian-transmission /home/djnitehawk/Ready

chmod 777 -R /home/djnitehawk/Downloads
chmod 777 -R /home/djnitehawk/Ready

echo "Folder prep done..."
```

save and exit nano by pressing CTRL+X and Y and enter.

and then run the following commands one after the other:

```
./prep-dirs.sh
sudo service transmission-daemon stop
sudo echo "" > /etc/transmission-daemon/settings.json
sudo nano /etc/transmission-daemon/settings.json
```

then copy and paste the following text into nano:

**note:** replace "djnitehawk" with your username.  
**note:** replace "YOUR_PASSWORD_GOES_HERE" with a password of your choice.

```
{
    "alt-speed-down": 1024, 
    "alt-speed-enabled": false, 
    "alt-speed-time-begin": 540, 
    "alt-speed-time-day": 127, 
    "alt-speed-time-enabled": false, 
    "alt-speed-time-end": 1020, 
    "alt-speed-up": 1024, 
    "bind-address-ipv4": "0.0.0.0", 
    "bind-address-ipv6": "::", 
    "blocklist-enabled": false, 
    "blocklist-url": "http://www.example.com/blocklist", 
    "cache-size-mb": 4, 
    "dht-enabled": false, 
    "download-dir": "/home/djnitehawk/Downloads/OTHER", 
    "download-limit": 100, 
    "download-limit-enabled": 0, 
    "download-queue-enabled": true, 
    "download-queue-size": 3, 
    "encryption": 1, 
    "idle-seeding-limit": 60, 
    "idle-seeding-limit-enabled": false, 
    "incomplete-dir": "", 
    "incomplete-dir-enabled": false, 
    "lpd-enabled": true, 
    "max-peers-global": 300, 
    "message-level": 2, 
    "peer-congestion-algorithm": "", 
    "peer-limit-global": 300, 
    "peer-limit-per-torrent": 100, 
    "peer-port": 54321, 
    "peer-port-random-high": 65535, 
    "peer-port-random-low": 43211, 
    "peer-port-random-on-start": false, 
    "peer-socket-tos": "default", 
    "pex-enabled": false, 
    "port-forwarding-enabled": false, 
    "preallocation": 0, 
    "prefetch-enabled": 1, 
    "queue-stalled-enabled": true, 
    "queue-stalled-minutes": 60, 
    "ratio-limit": 5, 
    "ratio-limit-enabled": false, 
    "rename-partial-files": true, 
    "rpc-authentication-required": true, 
    "rpc-bind-address": "0.0.0.0", 
    "rpc-enabled": true, 
    "rpc-password": "YOUR_PASSWORD_GOES_HERE", 
    "rpc-port": 12345, 
    "rpc-url": "/transmission/", 
    "rpc-username": "djnitehawk", 
    "rpc-whitelist": "127.0.0.1", 
    "rpc-whitelist-enabled": false, 
    "scrape-paused-torrents-enabled": true, 
    "script-torrent-done-enabled": true, 
    "script-torrent-done-filename": "/home/djnitehawk/tex/tex.sh", 
    "seed-queue-enabled": false, 
    "seed-queue-size": 10, 
    "speed-limit-down": 1024, 
    "speed-limit-down-enabled": false, 
    "speed-limit-up": 1024, 
    "speed-limit-up-enabled": false, 
    "start-added-torrents": true, 
    "trash-original-torrent-files": true, 
    "umask": 0, 
    "upload-limit": 1024, 
    "upload-limit-enabled": 0, 
    "upload-slots-per-torrent": 100, 
    "utp-enabled": true, 
    "watch-dir": "", 
    "watch-dir-enabled": false
}
```

save and exit nano by pressing CTRL+X and Y and enter.

and then run the following commands one after the other:

```
sudo service transmission-daemon start
rm prep-dirs.sh
```

----

**PREPARE THE POSTPROCESSING SCRIPT**

run the following commands one after the other:

```
cd ~/
sudo apt-get install unrar
sudo apt-get install curl
mkdir tex
cd tex
echo "" > tex.sh
nano tex.sh
```

then copy and paste the following text into nano:

**note:** replace these with your information:
- `djnitehawk`
- `YOUR_PASSWORD_GOES_HERE`
- `MY_EMAIL@EMAIL_DOMAIN.COM`
- `MY_BOXCAR_API_KEY`

``` /bin/bash
#!/bin/bash

OLD_IFS="$IFS"
IFS=$'\n'
sleep 10s

MOV_DIR="/home/djnitehawk/Ready/MEDIA/MOVIES"
XXX_DIR="/home/djnitehawk/Ready/MEDIA/STORAGE"
TVS_DIR="/home/djnitehawk/Ready/MEDIA/TV-SHOWS"
ELS_DIR="/home/djnitehawk/Ready/Completed"
LOG_FILE="/home/djnitehawk/tex/tex.log"
TR_SERVER="127.0.0.1:12345"
TR_USERNAME="djnitehawk"
TR_PASSWORD="YOUR_PASSWORD_GOES_HERE"
EMAIL="MY_EMAIL@EMAIL_DOMAIN.COM"
BOX_KEY="MY_BOXCAR_API_KEY"

SRC_DIR="$TR_TORRENT_DIR/$TR_TORRENT_NAME"
TMP_DIR="$SRC_DIR/tmp"
DST_DIR="$ELS_DIR/$TR_TORRENT_NAME"

if [[ "$TR_TORRENT_DIR" == *RATIO* ]] ; then
  echo " " >> "$LOG_FILE"
  echo "Skiped: $TR_TORRENT_NAME" >> "$LOG_FILE"
  exit 0
fi

if [[ "$TR_TORRENT_DIR" == *MOVIES* ]] ; then
  DST_DIR="$MOV_DIR/$TR_TORRENT_NAME"
fi

if [[ "$TR_TORRENT_DIR" == *STORAGE* ]] ; then
  DST_DIR="$XXX_DIR/$TR_TORRENT_NAME"
fi

if [[ "$TR_TORRENT_DIR" == *TV-SHOWS* ]] ; then
  DST_DIR="$TVS_DIR/$TR_TORRENT_NAME"
fi

cd "$TR_TORRENT_DIR"

if [ -d "$SRC_DIR" ]; then

  unset RAR_FILES i
  for RAR in $(find "$SRC_DIR" -type f -iname "*.rar"); do
    if [[ "$RAR" == *.part*.rar ]]; then
      if [[ "$RAR" =~ .*part0*1.rar ]] || [[ "$RAR" =~ .*part1.rar ]]; then
        RAR_FILES[i++](/i++)="$RAR"
      fi
    else
      RAR_FILES[i++](/i++)="$RAR"
    fi
  done
  
  rm -f -R "$DST_DIR"
  mkdir "$DST_DIR"

  if [ ${#RAR_FILES[@](/@)} -gt 0 ]; then
    rm -f -R "$TMP_DIR"
    mkdir "$TMP_DIR"
    find "$SRC_DIR" -type f  ! -name "*.r??" -execdir cp {} "$TMP_DIR" \;
    for RAR_FILE in "${RAR_FILES[@](/@)}"; do
      unrar x "$RAR_FILE" "$TMP_DIR"
      if [ $? -gt 0 ]; then
		rm -f -R "$TMP_DIR"
		echo " " >> "$LOG_FILE"
		echo "Error : $TR_TORRENT_NAME. Will verify and restart torrent..." >> "$LOG_FILE"
		BOXCAR="http://boxcar.io/devices/providers/$BOX_KEY/notifications"
		curl -d "email=$EMAIL" -d "&notification[from_screen_name](/from_screen_name)=TEX" -d "&notification[message](/message)=Unrar Failed: $TR_TORRENT_NAME" "$BOXCAR"
		transmission-remote $TR_SERVER --auth $TR_USERNAME:$TR_PASSWORD -t$TR_TORRENT_ID --stop
		sleep 10s
		transmission-remote $TR_SERVER --auth $TR_USERNAME:$TR_PASSWORD -t$TR_TORRENT_ID --verify
		sleep 10s
		transmission-remote $TR_SERVER --auth $TR_USERNAME:$TR_PASSWORD -t$TR_TORRENT_ID --start
		IFS="$OLD_IFS"
		rm -f -R "$DST_DIR"
		exit 0
      fi
    done
    sleep 10s
    mv --target-directory="$DST_DIR" "$TMP_DIR"/*
    rm -f -R "$TMP_DIR"
    chmod 777 -R "$DST_DIR"
    echo " " >> "$LOG_FILE"
    echo "Unrard: $TR_TORRENT_NAME" >> "$LOG_FILE"
  else
    cp -r --target-directory="$DST_DIR" "$SRC_DIR"/*
    chmod 777 -R "$DST_DIR"
    echo " " >> "$LOG_FILE"
    echo "Copied: $TR_TORRENT_NAME" >> "$LOG_FILE"
  fi

  find "$DST_DIR" -type f \( -name "*sample*.avi" -o -name "*sample*.mp4" -o -name "*sample*.mkv" \) -delete
fi

if [ -f "$SRC_DIR" ]; then
  cp --remove-destination "$SRC_DIR" "$DST_DIR"
  chmod 777 "$DST_DIR"
  echo " " >> "$LOG_FILE"
  echo "Copied: $TR_TORRENT_NAME" >> "$LOG_FILE"
fi

IFS="$OLD_IFS"
```

save and exit nano by pressing CTRL+X and Y and enter.

and then run the following command:

```
chmod 777 tex.sh
```

----

**PREPARE FLEXGET**

run the following commands one after the other:

```
cd ~/
sudo apt-get install python-pip
sudo pip install flexget
easy_install transmissionrpc
cd .flexget
echo "" > config.yml
nano config.yml
```

then copy and paste the following text into nano:

**note:** replace these with your information:
- `djnitehawk`
- `YOUR_PASSWORD_GOES_HERE`
- `YOUR_THETVDB_ACCOUNT_ID`
- `MY_EMAIL@EMAIL_DOMAIN.COM`
- `MY_BOXCAR_API_KEY`
- `YOUR_IMDB_USERNAME`
- `YOUR_IMDB_PASSWORD`
- `YOUR_IMDB_HDWATCHLIST_ID`
- `XXXXX`

```
templates:
  tv:
    transmission:
      host: localhost
      port: 12345
      username: djnitehawk
      password: YOUR_PASSWORD_GOES_HERE
      addpaused: no
      path: /home/djnitehawk/Downloads/TV-SHOWS
    regexp:
      reject:
        - mSD
        - AFG
    import_series:
      settings:
        quality: hdtv <720p
        propers: no
      from:
        thetvdb_favorites:
          account_id: YOUR_THETVDB_ACCOUNT_ID
          strip_dates: yes
    exec: curl -s -d "email=MY_EMAIL@EMAIL_DOMAIN.COM" -d "&notification[from_screen_name](/from_screen_name)=FlexGet" -d "&notification[message](/message)={{title}}" http://boxcar.io/devices/providers/MY_BOXCAR_API_KEY/notifications

  movie:
    transmission:
      host: localhost
      port: 12345
      username: djnitehawk
      password: YOUR_PASSWORD_GOES_HERE
      addpaused: no
      path: /home/djnitehawk/Downloads/MOVIES
    movie_queue: yes
    seen_movies: strict
    proper_movies: no
    exec: curl -s -d "email=MY_EMAIL@EMAIL_DOMAIN.COM" -d "&notification[from_screen_name](/from_screen_name)=FlexGet" -d "&notification[message](/message)={{title}}" http://boxcar.io/devices/providers/MY_BOXCAR_API_KEY/notifications

tasks:
  ipt-tv:
    rss:
      url: http://www.XXXXX.com/torrents/rss?download;l78;l66;l79;l5;l4;u=XXXXX;tp=XXXXX
      all_entries: no
    template: tv
    priority: 1

  imdb-watchlist:
    imdb_list:
      username: YOUR_IMDB_USERNAME
      password: YOUR_IMDB_PASSWORD
      list: watchlist
    accept_all: yes
    queue_movies:
      quality: dvdrip|bluray xvid|divx <720p
    priority: 2

  hd-watchlist:
    imdb_list:
      username: YOUR_IMDB_USERNAME
      password: YOUR_IMDB_PASSWORD
      list: YOUR_IMDB_HDWATCHLIST_ID
    accept_all: yes
    queue_movies:
      quality: dvdrip|bluray xvid|divx|h264 720p
    priority: 3

  ipt-movies:
    rss:
      url: http://www.XXXXX.com/torrents/rss?download;l48;l62;l7;l77;u=XXXXX;tp=XXXXX
      all_entries: no
    template: movie
    priority: 4
```

save and exit nano by pressing CTRL+X and Y and enter.

and then run the following command to check if the config file has any errors:
if any errors are found, edit the config.yml again and double check your work.

```
flexget --check
```

----

**PREPARE THE CRON SCRIPT**

first run the following command and note down the full path to the flexget binary:

```
which flexget
```

then run the following commands one after the other:

```
cd ~/.flexget
echo "" > cron.sh
chmod 777 cron.sh
nano cron.sh
```

then copy and paste the following text into nano:

**note:** replace "djnitehawk", "MY_EMAIL@EMAIL_DOMAIN.COM", "MY_BOXCAR_API_KEY" with your information.  
**note:** also check if the path of the flexget binary (/usr/local/bin/flexget) is the same as the output from the "which flexget" command you ran earlier. if not, change it in the script below after pasting it into nano.

```/bin/bash

EMAIL="MY_EMAIL@EMAIL_DOMAIN.COM"
BOX_KEY="MY_BOXCAR_API_KEY"
FILE="/home/djnitehawk/.flexget/.config-lock"
LOG="/home/djnitehawk/.flexget/cron.log"

F=$(pidof -s -x flexget)
T=$(pidof -s -x transmission-daemon)

if [ $F ]; then
	kill $F
	echo "flexget was still running... so killed it..." >> $LOG
fi

if [ -f $FILE ]; then
	echo "lock file was there. so deleting lock file..." >> $LOG
	rm -f $FILE
fi

if [ -z $T ]; then
	echo "transmission is not running... calling dj nitehawk now..." >> $LOG
	BOXCAR="http://boxcar.io/devices/providers/$BOX_KEY/notifications"
	curl -d "email=$EMAIL" -d "&notification[from_screen_name](/from_screen_name)=FLEX-CRON" -d "&notification[message](/message)=Transmission isn't running. Please restart VPS." $BOXCAR
else
	D=$(date)
	echo "$D - running flexget cron now..." >> $LOG
	echo " "
	/usr/local/bin/flexget --cron
fi

exit 0
```

save and exit nano by pressing CTRL+X and Y and enter.

then run the following command:

```
crontab -e
```

then copy and paste the following line (at the end) into nano:

**note:** replace "djnitehawk" with your username.

```
*/30 * * * * /home/djnitehawk/.flexget/cron.sh
```

save and exit nano by pressing CTRL+X and Y and enter.

now run flexget manually in verbose mode to see if everything is running ok:

```
flexget --verbose
```

that's all you need to automate your torrents with flexget and transmission. you can keep adding new movies and tv shows to your watchlists on imdb and thetvdb sites and flexget will automatically keep an eye out for matching torrents that comes out in the future and download them for you.

once transmission finishes a torrent, give a bit of time for the postprocessing script to send the extracted content to your "Ready" folder (/home/djnitehawk/Ready). you can download and remove any torrent from the "Ready" folder without having to worry about seeding the original torrent as it is a separate copy from the original torrent data. once you finish seeding a torrent in transmission, simply right click a torrent and choose "trash data and remove from list" in the webui or remote clients and your disk space will be freed up.

the following section will describe how to setup an automated download manager which will grab everything from the "Ready" folder with the directory structure intact. Once a file is downloaded, it will remove the file from the VPS/SB to free up space. once, all files from the "Ready" folder are downloaded, it will clean up any empty folders from the VPS/SB also.

----

**PREPARE THE DOWNLOAD MANAGER SCRIPT**

the download manager setup has been moved to a separate page here: [Download Manager Setup](/Cookbook/Transmission/DownloadManagerSetup)

----

**MISC STUFF**

if/when you get a notification saying that transmission is not running, you have to do the following to make sure you wont miss any torrents:

```
1) start the transmission daemon manually or restart the machine.
2) edit your config.yml and find and replace "all_entries: no" with "all_entries: yes"
3) run flexget once manually
4) undo the change u did above to your config.yml
```

if you have a firewall enabled on your VPS/SB, make sure the following ports are open for business:

```
port: 80 (web server)
port: 54321 (transmission daemon)
port: 12345 (transmission webui/remote/clients)
```

----

**FEEDBACK & SUPPORT:**

if you have any questions or have any ideas to improve this recipe, please send me a message via [facebook](http://djnitehawk.com) and i will try my best to get back to you. no guarantees though :-)
----

[Back to The Cookbook](/Cookbook)