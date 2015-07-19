== bash one-liners ==

Place these in .bashrc or (preferably) .bash_aliases, located in your $HOME directory in Linux, next to your .flexget directory

'''flexget.log parsers'''

The following quick functions leverage the Verbose Logging Plugin (''plugins/plugin_verbose_details.py''), and in this case it works very well with the Transmission plugin (''plugins/plugin_transmission.py''), or any other that writes a line to the log for each accepted item (a standard type of operation).

==== Helper method to parse the log files ====

Parses log files for any Accepted items, and groups each batch of them together in a summary.

{{{
# Helper alias to display recent flexget activity summaries
fxl() {  cat $HOME/.flexget/flexget.log | awk '$0 ~ /Summary - Accepted:/ && $9 > 0 {x=NR+$9}(NR<=x){if(NR==x)print $0 RS "- - - -"; else print; fi; }'; }
}}}


[[BR]]
==== The same Helper method, but for ''all'' log files  ====

The same as above but for all of the log files still in rotation inside the .flexget folder.

{{{
# Helper alias to display recent flexget activity summaries from ALL logs
fxla() { cat $HOME/.flexget/flexget.lo* | awk '$0 ~ /Summary - Accepted:/ && $9 > 0 {x=NR+$9}(NR<=x){if(NR==x)print $0 RS "- - - -"; else print; fi; }'; }
}}}