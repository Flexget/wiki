= TransmissionRPC =

Passes the url of an entry to Transmission bittorrent client. Can also pass magnet links to Transmission. 

This plugin requires the transmissionrpc libs from http://bitbucket.org/blueluna/transmissionrpc

until version 0.4 is released you need to download the development release which could be done from the get source menu. 

unpack the source.

to install it as root go to transmissionrpc/ directory and do:

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