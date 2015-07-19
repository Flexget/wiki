==== bash one-liners ====

Place these in .bashrc or (preferably) .bash_aliases, located in your $HOME directory in Linux, next to your .flexget directory

'''flexget.log parsers'''

Helper method to parse the log files for Accepted items, and groups them together

{{{
# Helper alias to display recent flexget activity summaries
fxl() {  cat $HOME/.flexget/flexget.log | awk '$0 ~ /Summary - Accepted:/ && $9 > 0 {x=NR+$9}(NR<=x){if(NR==x)print $0 RS "- - - -"; else print; fi; }'; }
}}}


[[BR]]
The same as above but for all log files still in rotation inside the .flexget folder

{{{
# Helper alias to display recent flexget activity summaries from ALL logs
fxla() { cat $HOME/.flexget/flexget.lo* | awk '$0 ~ /Summary - Accepted:/ && $9 > 0 {x=NR+$9}(NR<=x){if(NR==x)print $0 RS "- - - -"; else print; fi; }'; }
}}}