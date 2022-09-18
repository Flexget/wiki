---
title: anon
description: 
published: true
date: 2022-09-18T05:19:33.429Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:19:30.730Z
---

After quite extensive research and help from the good people in Freenode/#flexget i have now created a few scripts that make life a lot easier.

The user defines what it wants to watch via trakt.tv, or imdb.com.
Each time the script is executed it reads the RSS feeds provided, and if something is matched, adds it to deluge.
If a user adds something old, it will use private or public trackers defined to acquire the content.

To be able to archive and store media and still seed it if it's in rar format, the deluge execute plugin is used together with a script.
The script will determine in what state the content is in (.mkv , .rar or other format), and unrar/copy it accordingly to its archive location.
This allows you to extract media and still allow the torrent to seed.

Finally a crontab allows you to periodically email yourself what has been downloaded between each report.

#############################################################################

FLEXGET config.yml: 
everything in with CHANGE-infront needs to be replaced

#############################################################################
```
templates:
  DELUGE:
    deluge:
      username: CHANGE-DELUGEUSERNAME
      password: CHANGE-DELUGEPASSWORD
      main_file_only: yes
      keep_subs: yes
      ratio: 3
      removeatratio: yes
      maxupspeed: 10000.0
      maxdownspeed: 15000.0
        

  RSS-SERIES:
    inputs:
    - rss: CHANGE-MYRSSFEEDSFORSERIES-1
    - rss: CHANGE-MYRSSFEEDSFORSERIES-2
    
  RSS-MOVIES:
    inputs:
    - rss: CHANGE-MYRSSFEEDSFORMOVIES-1
    - rss: CHANGE-MYRSSFEEDSFORMOVIES-2
    
  TRAKT-SERIES:
    configure_series:
      settings:
        quality: 720p
      from:
        inputs:
        - trakt_list:
            username: CHANGE-USERNAME-1
            list: watchlist
            type: shows
        - trakt_list:
            username: CHANGE-USERNAME-2
            list: watchlist
            type: shows        
    metainfo_series: yes

tasks:
  SERIES:
    priority: 1
    template:
      - DELUGE
      - RSS-SERIES
      - TRAKT-SERIES
    set:
      path: '/media/incoming/' # CHANGE TO WHATEVER PATH YOU PREFER
          
        
  QUEUE-MOVIES:
    priority: 2
    inputs:
    - trakt_list:
        username: CHANGE-USERNAME-1
        list: watchlist
        type: movies
    - trakt_list:
        username: CHANGE-USERNAME-1
        list: watchlist
        type: movies
    - imdb_list:
        user_id: CHANGE-USERID-1
        list: watchlist
    - imdb_list:
        user_id: CHANGE-USERID-2
        list: watchlist
    accept_all: yes
    movie_queue: add
    exists_movie:
      path: /media/plex/hdtv/   # REPLACE WITH WHERE YOUR MOVIE ARCHIVE IS KEPT, THIS DETECTS MOVIES YOU ALREADY HAVE INSTEAD OF DOWNLOADING THEM AGAIN.
      type: dirs
      allow_different_qualities: no
      lookup: imdb

  MOVIES:
    priority: 3
    movie_queue: accept
    template:
      - RSS-MOVIES
      - DELUGE
    quality: 1080p
    set:
      path: '/media/incoming/'  # CHANGE TO WHATEVER YOU PREFER

  MOVIES-BACKFILL:
    priority: 10
    torrent_alive: 10
    template:
      - DELUGE
    discover:
      what:
        - emit_movie_queue: yes
      from:
        - piratebay:
            category: "highres movies"
            sort_by: seeds
      interval: 7 days
    quality: 1080p bluray h264
    movie_queue: accept
    set:
      path: '/media/incoming/'  # CHANGE TO WHATEVER YOU PREFER

```

#############################################################################

UNRAR and COPY execute.php script: 
in deluge, activate the "execute" plugin. Add a rule to execute this script each time a download finishes. Deluge seems to have to be restarted to activate the rule.

#############################################################################

```/usr/bin/php
<?php


/*--------------------------------------------------------*

	Change these variables to suite your needs
	$movie_path is the location where you want your movies to be permanently stored
	$tv_path is the location where you want your tv-series to be permanently stored
	$list_path is the location of a file with a list of the daily downloads, the content can then be emailed once a day.
	$logfile is the file where everything is logged to.

/--------------------------------------------------------*/

$movie_path = "/media/plex/movies/";
$tv_path = "/media/plex/tvseries/";
$list_path = "/var/lib/deluge/list";
$logfile = "/var/log/sort";

/*--------------------------------------------------------*

	Nothing below here should have to be modified.

/--------------------------------------------------------*/

//log each command run to be able to trace any problems, use grep to grep the PID if multiple executes run at the same time.
function logger($message) {
	$date = date('Y-m-d H:i:s');
	file_put_contents($logfile, $date." ".getmypid()." ".$message."\n", FILE_APPEND | LOCK_EX);
}

//log and execute all the commands, escaping the shell commands for anything dangerous.
function logexec($cmd) {

// get an array of all arguments passed to function
$args = func_get_args();

// remove the first cell
array_shift($args);

//escape shell arguments from each cell
$args = array_map("escapeshellarg", $args);

//make the array back to a string
$cmd.=" ".implode($args," ");

//log and execute
logger($cmd);
echo $cmd."\n";
exec($cmd);
}

//deluge feeds execute scripts with 3 arguments, torrentid, torrentname, and torrentpath.
$torrent_id = $argv[1](/1);
$torrent_name = $argv[2](/2);
$torrent_path = $argv[3](/3);

//this writes each item downloaded to a file, where the content can later be emailed as a daily summary.
file_put_contents($list_path, date('Y-m-d H:i:s')." ".$torrent_name."\n", FILE_APPEND | LOCK_EX);

// check if its a tv-series or movie
$tv_or_movie = preg_match('/^(.*)((\d+)[ex](/ex)(\d+))/i', strtolower($torrent_name) , $matches);

logger('--- BEGIN --- : '.implode($argv,' '));

if ( empty($matches) ) {
	// if it's in non-unix format with whitespaces, remove these..
	$target = $movie_path.str_replace(' ', '_',$torrent_name);
	logexec("mkdir", $target);
	
	if ( glob($torrent_path.$torrent_name."/*.mkv") ) {
		logger("movie is already in mvk format, copying: ".$target);
		logexec("cp ".escapeshellarg($torrent_path.$torrent_name)."/*.mkv", $target);
	} else if ( glob($torrent_path.$torrent_name."/*.rar") ) {
		logger("movie is in rar format, extracting: ".$target);
		logexec("unrar e -y", $torrent_path.$torrent_name, $target);
	} else {
		logger("this is not in mkv or rar format, possibly mp4 so copying everything");
		logexec("cp ".escapeshellarg($torrent_path.$torrent_name)."/*", $target);
	}

	$esc_source = escapeshellarg($torrent_path.$torrent_name);

	logexec("cp ".$esc_source."/*.nfo", $target);
	logexec("cp ".$esc_source."/Subs/*", $target);
	logexec("cp ".$esc_source."/subs/*", $target);
	logexec("unrar e -y", $target, $target."/");
	logexec("unrar e -y", $target, $target."/");

	logger("cleaning up...");
	logexec("rm -rf ".escapeshellarg($target)."/*.rar");
	logexec("rm -rf ".escapeshellarg($target)."/*.sfv");

} else {
	
	if ( preg_match('/^(.*)s(\d+)[e](/e)(\d+)/i', strtolower($torrent_name), $res) ) {
		$name = trim($res[1](/1), ".");
		$season = str_pad($res[2](/2), 2, "0", STR_PAD_LEFT);
		$episode = str_pad($res[3](/3), 2, "0", STR_PAD_LEFT);
	}

	if ( preg_match('/^(.*)(\d+)[x](/x)(\d+)/i', strtolower($torrent_name), $res) ) {
		$name = trim($res[1](/1), ".");
		$season = str_pad($res[2](/2), 2, "0", STR_PAD_LEFT);
		$episode = str_pad($res[3](/3), 2, "0", STR_PAD_LEFT);
	}

	logexec( "mkdir -p", $tv_path.$name."/season.".$season."/".$torrent_name );
	logexec( "unrar e -y", $torrent_path.$torrent_name, $tv_path.$name."/season.".$season."/".$torrent_name);
	logexec( "cp ".escapeshellarg($torrent_path.$torrent_name)."/*.nfo", $tv_path.$name."/season.".$season."/".$torrent_name);
}

logger('--- END ---');

?>

```

#############################################################################

CRONTAB:
optionally, email yourself the content of 'list' at intervals, below example is each day at 17.00

#############################################################################

```
0 17 * * * cat /var/lib/deluge/list | mail -s 'daily viewing' userlist ; rm /var/lib/deluge/list

```