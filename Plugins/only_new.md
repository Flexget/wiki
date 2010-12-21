= Only New =

This plugin prevents all entries that were in the feed on the previous run to be rejected at the input event.

This should not be needed on most feeds, and may cause problems in instances where processing an entry on the second run is desired (e.g. entry failed on first run, lookup was not available first run.) It is most helpful in cases where performance is an issue.

'''Example:'''

{{{
only_new: yes
}}}