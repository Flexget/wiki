= Clean Transmission =
This plugin cleans the Transmission's queue of finished torrents (=the torrents that have completed the download process and are in '''stopped, finished or seeding''' state).

This plugin requires the transmissionrpc library. To install it, run:

{{{
easy_install transmissionrpc
}}}

You may be required to upgrade transmissionrpc after upgrading transmission, for that just add `--upgrade` to the previous command.

'''Example:'''

{{{
clean_transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
  finished_for: 2 hours
  min_ratio: 1
  disable_builtins: [details]
}}}

||'''Name'''||'''Info'''||'''Description'''||
||host||Text||Where transmission is listening (default: localhost)||
||port||Number||Connected port (default: 9091)||
||netrc||File||||
||username||Text||||
||password||Text||||
||finished_for||Interval||(optional) remove only torrents finished for at least the specified time (1 hours, 2 days, etc).||
||min_ratio||Number||(optional) remove only torrents uploaded at least this ratio (0=0%, 0.5=50%, 1=100% etc)||
||enabled||[Yes|No]||Plugin enabled (default: yes)||

'''Note:'''

- If `finished_for` and/or `min_ratio` parameters are defined, all the finished torrents meeting one or both the conditions will be removed.
- `disabled_builtins: [details] this plugins triggers default warnings that will be shown in flexget.log. This disables those warnings. 