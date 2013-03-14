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
}}}