= From Transmission =
This plugin creates an entry for each item you have loaded in transmission.

This plugin requires the transmissionrpc library. To install it, run:

{{{
easy_install transmissionrpc
}}}

You may be required to upgrade transmissionrpc after upgrading transmission, for that just add `--upgrade` to the previous command.

'''Example:'''

{{{
from_transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
}}}

||'''Name'''||'''Info'''||'''Description'''||
||host||Text||Where transmission is listening (default: localhost)||
||port||Number||Connected port (default: 9091)||
||netrc||File||||
||username||Text||||
||password||Text||||
||onlycomplete||[yes|no]||If this is enabled, only completed torrents will have entries created.||
