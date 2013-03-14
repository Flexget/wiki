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

and then run the following commands one after the other: