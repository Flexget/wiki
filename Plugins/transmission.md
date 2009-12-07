= TransmissionRPC =

Passes the url of an entry to Transmission bittorrent client. Can also pass magnet links to Transmission. 

This plugin requires the transmissionrpc libs from http://bitbucket.org/blueluna/transmissionrpc

until version 0.4 is released you need to download the development release:

install mercurial from http://mercurial.selenic.com/ (or use you packetmanager)

then:

hg clone http://bitbucket.org/blueluna/transmissionrpc/

to install it as root go to transmissionrpc/ dir and do:

python ./setup.py install

'''Example:'''

{{{
transmissionrpc:
  host: localhost
  port: 9091
  netrc: /home/flexget/.tmnetrc
  username: myusername
  password: mypassword
}}}