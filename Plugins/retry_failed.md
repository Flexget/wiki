= Retry Failed =
This plugin serves several purposes. It will save failed entries in the backlog, to make sure they can be retried even if they scroll out of your input. It also enforces an interval before retrying again, so that other possibly acceptable entries may be grabbed in place of the failing entry. Lastly, it rejects entries that have failed more than a certain number of times.

By default, there is a 1 hour wait time in between retries of failed entries. This will be increased by 1.5 times on each successive failure of the entry. By default, entries will be retried 3 times, (meaning 4 total failures are possible.)

This plugin is a [wiki:Builtin builtin] and does not need to be explicitly placed in your feed unless you would like to override the defaults. Here is an example of overriding the defaults:
{{{
retry_failed:
  retry_time: 30 minutes # Base time in between retries
  retry_time_multiplier: 2 # Amount retry time will be multiplied by after each successive failure
  max_retries: 5 # Number of times the entry will be retried
}}}

Command line argument `--clear` can be used to clear list and retry items currently in the feed.