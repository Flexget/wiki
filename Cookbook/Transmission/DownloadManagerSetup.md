---
title: DownloadManagerSetup
description: 
published: true
date: 2022-09-18T05:22:16.066Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:22:13.329Z
---

## Download Manager Setup
this is a continuation of the [recipe for setting up flexget with transmission client. ](/Cookbook/Transmission)  
please refer to that recipe if you are interested in how to setup flexget & transmission for automating your torrenting.

this page alone will not be of much use to you unless you are an advanced user.
----
**PREPARE THE WEB SERVER**

on your VPS/seedbox, run the following commands one after the other:
```
sudo apt-get install lighttpd
sudo apt-get install php5-cgi
sudo nano "" > /etc/lighttpd/lighttpd.conf
sudo nano /etc/lighttpd/lighttpd.conf
```
then copy and paste the following text into nano:

**note:** replace "djnitehawk" with your username
```
server.modules = (
	"mod_access",
	"mod_alias",
	"mod_compress",
 	"mod_redirect",
	"mod_auth",
	"mod_fastcgi",
#       "mod_rewrite",
)

server.document-root        = "/home/djnitehawk/Ready"
server.upload-dirs          = ( "/var/cache/lighttpd/uploads" )
server.errorlog             = "/var/log/lighttpd/error.log"
server.pid-file             = "/var/run/lighttpd.pid"
server.username             = "www-data"
server.groupname            = "www-data"

index-file.names            = ( "index.php", "index.html",
                                "index.htm", "default.htm",
                               " index.lighttpd.html" )

url.access-deny             = ( "~", ".inc" )

static-file.exclude-extensions = ( ".php", ".pl", ".fcgi" )

## Use ipv6 if available
#include_shell "/usr/share/lighttpd/use-ipv6.pl"

dir-listing.encoding        = "utf-8"
server.dir-listing          = "disable"

compress.cache-dir          = "/var/cache/lighttpd/compress/"
compress.filetype           = ( "application/x-javascript", "text/css", "text/html", "text/plain" )

include_shell "/usr/share/lighttpd/create-mime.assign.pl"
include_shell "/usr/share/lighttpd/include-conf-enabled.pl"

auth.debug = 0
auth.backend = "plain"
auth.backend.plain.userfile = "/etc/lighttpd/pass.txt"
auth.require = ( "/" =>
(
"method" => "basic",
"realm" => "Password protected area... Get lost!",
"require" => "user=djnitehawk"
)
)

fastcgi.server = ( ".php" => (( 
				"bin-path" => "/usr/bin/php5-cgi",
				"socket" => "/tmp/php.socket" 
				)))

```
save and exit nano by pressing CTRL+X and Y and enter.

and then run the following command:
```
sudo nano /etc/lighttpd/pass.txt
```
then copy and paste the following text into nano:

**note:** replace "djnitehawk" with your username and replace "A_STRONG_PASSWORD_FOR_YOUR_WEB_SERVER" with a strong password.
```
djnitehawk:A_STRONG_PASSWORD_FOR_YOUR_WEB_SERVER
```
save and exit nano by pressing CTRL+X and Y and enter.

and then run the following commands one after the other:
```
sudo chmod 777 /etc/lighttpd/pass.txt
sudo openssl req -new -x509 -keyout server.pem -out server.pem -days  36500 -nodes
```
at this point, it will ask you for some personal details. just enter the appropriate values for generating your own self signed SSL certificate. pay special attention when it asks for your "**Common Name (e.g. server FQDN or YOUR name)**". you have to enter your domain or subdomain name you have setup for your VPS/seedbox. i have not tried entering an IP address in this field, but you can try.

after the wizard finishes, run the following commands one after the other:

```
sudo chmod 777 server.pem
sudo mv server.pem /etc/lighttpd/
sudo lighty-enable-mod ssl
nano ~/Ready/index.php
```
then copy and paste the following text into nano:

**note:** replace "djnitehawk" with your username.
```
<?php

$src = "/home/djnitehawk/Ready";

$del = $_GET[delete](/delete);
$clean = $_GET[clean](/clean);

if (!empty($del)){
	$file = "$src$del";
	unlink($file);
	echo "File Deleted: $file";
	exit;
}

if (!empty($clean)){
	if ($clean == 'yes') {
		RemoveEmptySubFolders($src);
		echo "Empty folders have been cleaned...";
	}
	exit;
}

$res = ListIn($src, "$src/");
echo implode('|',$res);

function RemoveEmptySubFolders($path)
{
  $empty=true;
  foreach (glob($path.DIRECTORY_SEPARATOR."*") as $file)
  {
     $empty &= is_dir($file) && RemoveEmptySubFolders($file);
  }
  return $empty && rmdir($path);
}

function ListIn($dir, $prefix) {
  $dir = rtrim($dir, '\\/');
  $result = array();

    foreach (scandir($dir) as $f) {
      if ($f !== '.' and $f !== '..' and $f !== '.lock' and $f !== 'index.php') {
        if (is_dir("$dir/$f")) {
          $result = array_merge($result, ListIn("$dir/$f", "$prefix$f/"));
        } else {
          $result[] = $prefix.$f;
        }
      }
    }

  return $result;
}

?>
```
save and exit nano by pressing CTRL+X and Y and enter.

and then run the following commands one after the other:
```
chmod 777 ~/Ready/index.php
sudo service lighttpd restart
```
that's all you have to do on your VPS/seedbox.

to verify that your newly installed web server is running with SSL, visit your VPS/seedbox in a web browser like so:
```
https://vps.mydomain.com
```
if everything works correctly, it should now prompt you for a username and password with some text like: "Password protected area... Get lost!" :-)

if it's not working, go back and double check your work. optionally try restarting your VPS/seedbox with:
```
sudo shutdown -r 0
```
----
**PREPARE THE LOCAL COMPUTER**

the following has to be done on your local ubuntu computer. if your local computer is a windows box, you can look into running ubuntu on a virtual machine (ex: http://www.virtualbox.org) until someone converts this whole recipe into windows.

ok, lets get started...

log into your local ubuntu box and run the followings commands one after the other:

```
sudo apt-add-repository ppa:t-tujikawa/ppa
sudo apt-get update
sudo apt-get install aria2
sudo apt-get install curl
cd ~/
nano downer
```
then copy and paste the following text into nano:

**note:** replace "djnitehawk", "FROM-SEEDBOX", "vps.mydomain.com", "A_STRONG_PASSWORD_FOR_YOUR_WEB_SERVER" with your information.
```/bin/bash

clear

SRC_DIR="/home/djnitehawk/Ready"
DST_DIR="/home/djnitehawk/FROM-SEEDBOX"
HTTP="https://vps.mydomain.com"
USR="djnitehawk"
PASS="A_STRONG_PASSWORD_FOR_YOUR_WEB_SERVER"

if [ -z $1 ]; then
	BW="0"
	LIST="no"
else
	if [ $1 == "list" ]; then
		BW="0"
		LIST="yes"
	else
		BW="${1}K"
		LIST="no"
	fi
fi

trap 'chmod 777 -R $DST_DIR;echo "Exiting...";exit;' SIGTERM SIGINT

echo " "
echo "Getting a list of files to download from server..."
echo " "

RES=$(wget --timeout=60 --waitretry=10 --tries=10 --no-check-certificate --user=$USR --password=$PASS -q -O - $HTTP)

OLDIFS="$IFS"
	IFS='|' read -a LST <<< "$RES"
IFS="$OLDIFS"

unset i
for F in "${LST[@](/@)}";do
	F=${F/$SRC_DIR/$HTTP}
	LST[i++](/i++)="$F"
done

if [ ${#LST[@](/@)} -eq 0 ]; then

	echo " "
	echo " "
	echo " "
	echo "No files received from server... So exiting..."
	exit 0

fi

if [ $LIST == "yes" ]; then
	clear
	echo " "
	echo "The list of files to be downloaded from the server:"
	echo "==================================================="
	
	unset i
	for FL in "${LST[@](/@)}";do
		FL=${FL/$HTTP/}
		MD="/MEDIA/"
		FL=${FL/$MD/}
		FL=$(dirname "$FL")
		GET_LST[i++](/i++)="$FL"
	done
	
	printf '\v\t%s\n' "${GET_LST[@](/@)}" | sort -u
	echo " "
		
	exit 0
fi

false

while [ $? -ne 0 ]; do
	
	ALL_OK=false
	c=1
	
	for FILE in "${LST[@](/@)}";do

		DEST=${FILE/$HTTP/$DST_DIR}
		DEST=$(dirname "$DEST")
		
		echo " "
		echo " "
		echo "Downloading file $c of ${#LST[@](/@)}..."
		echo " "
		echo "File: $FILE"
		echo " "
		echo " "
		echo " "		
		aria2c -d "$DEST" -c -k 1M -s 10 -x 10 -m 60 --retry-wait=60 --max-overall-download-limit=$BW --summary-interval=0 --check-certificate=false --http-user=$USR --http-passwd=$PASS "$FILE"
		if [ $? -ne 0 ]; then
			echo " "
			echo " "
			echo "Error: Something went wrong. Gonna retry..."
			echo " "
			TIME=$(date +%R)
			echo " " >> downer.log
			echo "$TIME - Failed: $FILE" >> downer.log
			break
		else
			ALL_OK=true
			echo " "
			echo " "
			echo "File downloaded fine. Deleting from server now..."
			echo " "
			DEL=${FILE/$HTTP\//}
			DEL_URL="$HTTP/?delete=/$DEL"
			echo " "
			wget --timeout=60 --waitretry=10 --tries=10 --no-check-certificate --user=$USR --password=$PASS -q -O - "$DEL_URL"
			echo " "
			echo " "
		fi
		
		c=$(($c+1))
	done
	
	if $ALL_OK ; then
		echo " "
		echo "Cleaning up empty folders from server. Please wait..."
		echo " "
		CLEAN="$HTTP/?clean=yes"
		wget --timeout=60 --waitretry=10 --tries=10 --no-check-certificate --user=$USR --password=$PASS -q -O - $CLEAN
		echo " "
		echo " "
		echo " "
		echo "All files have been downloaded and empty folders cleaned from server."
		echo " "
		echo "Run this script again to make sure no new files have been added to the server..."
		chmod 777 -R $DST_DIR
		true
	else
		false
	fi
	
done

read sdlkdjf
```
save and exit nano by pressing CTRL+X and Y and enter.

and then run the following command:
```
chmod +x downer
```
that's it. the setup is now complete...
----
to test the download manager, first make sure that your VPS/seedbox has some files in the "~/Ready" folder.

then log in to your local ubuntu box and issue the following command to start downloading files from your VPS/SB server:
```
./downer
```
to cancel the downloading, simply press CTRL+C

to display a list of files that are on the VPS/SB in the "~/Ready" folder, simply run:
```
./downer list
```
to limit the bandwidth used up by the download manager, simply run:
```
./downer 100
```
the 100 above is to set the download bandwidth limit to 100 KB/s. to limit the bandwidth to 1 MB/s, use 1024 like so:
```
./downer 1024
```
that's all there is to it... enjoy!!!
----
**TIPS & TRICKS**

to run the download manager in the background, so you can close/disconnect from your terminal session, use as follows:
```
screen -R x
./downer
```
at this point, you can either close your terminal session or detach from the download manager by pressing CTRL+A+D and it will still keep downloading your files from the VPS/SB.

to reconnect to an already running download manager, issue the screen command again like so:
```
screen -R x
```