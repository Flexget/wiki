== Download Manager Setup ==

this is a continuation of the [wiki:Cookbook/Transmission recipe for setting up flexget with transmission client. ][[BR]]
please refer to that recipe if you are interested in how to setup flexget & transmission for automating your torrenting.

this page alone will not be of much use to you unless you are an advanced user.
----
'''PREPARE THE WEB SERVER'''

on your VPS/seedbox, run the following commands one after the other:
{{{
sudo apt-get install lighttpd
sudo apt-get install php5-cgi
sudo nano "" > /etc/lighttpd/lighttpd.conf
sudo nano /etc/lighttpd/lighttpd.conf
}}}
then copy and paste the following text into nano:

'''note:''' replace "djnitehawk" with your username
{{{
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

}}}
save and exit nano by pressing CTRL+X and Y and enter.

and then run the following command:
{{{
sudo nano /etc/lighttpd/pass.txt
}}}
then copy and paste the following text into nano:

'''note:''' replace "djnitehawk" with your username and replace "A_STRONG_PASSWORD_FOR_YOUR_WEB_SERVER" with a strong password.
{{{
djnitehawk:A_STRONG_PASSWORD_FOR_YOUR_WEB_SERVER
}}}
save and exit nano by pressing CTRL+X and Y and enter.

and then run the following commands one after the other:
{{{
sudo chmod 777 /etc/lighttpd/pass.txt
sudo openssl req -new -x509 -keyout server.pem -out server.pem -days  36500 -nodes
}}}
at this point, it will ask you for some personal details. just enter the appropriate values for generating your own self signed SSL certificate. pay special attention when it asks for your "'''Common Name (e.g. server FQDN or YOUR name)'''". you have to enter your domain or subdomain name you have setup for your VPS/seedbox. i have not tried entering an IP address in this field, but you can try.

after the wizard finishes, run the following commands one after the other:

'''note:''' replace "djnitehawk" with your username.
{{{
sudo chmod 777 server.pem
sudo mv server.pem /etc/lighttpd/
sudo lighty-enable-mod ssl
nano ~/Ready/index.php
}}}
then copy and paste the following text into nano:

'''note:''' replace "djnitehawk" with your username.
{{{
<?php

$src = "/home/djnitehawk/Ready";

$del = $_GET['delete'];
$clean = $_GET['clean'];

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
}}}
save and exit nano by pressing CTRL+X and Y and enter.

and then run the following commands one after the other:
{{{
chmod 777 ~/Ready/index.php
sudo service lighttpd restart
}}}
that's all you have to do on your VPS/seedbox.

to verify that your newly installed web server is running with SSL, visit your VPS/seedbox in a web browser like so:
{{{
https://vps.mydomain.com
}}}
if everything works correctly, it should now prompt you for a username and password with some text like: "Protected Area. Get Lost." :-)

if it's not working, go back and double check your work. optionally try restarting your VPS/seedbox with:
{{{
sudo shutdown -r 0
}}}
----
'''PREPARE THE LOCAL COMPUTER'''

the following has to be done on your local ubuntu computer. if your local computer is a windows box, you can look into running ubuntu on a virtual machine (ex: http://www.virtualbox.org) until someone converts this whole recipe into windows.