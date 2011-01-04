= Only New =

This plugin causes all entries that were in the feed on the previous run* to be rejected at the input event.[[BR]]
^^^''*Except entries that were accepted and failed''^^^

This should not be needed on most feeds, and may cause problems in instances where processing an entry on the second run is desired (e.g. lookup was not available first run.) It is most helpful in cases where performance is an issue.

'''Example:'''

{{{
only_new: yes
}}}

You can disable only_new for a single run with the {{{--no-only-new}}} cli option. In addition, only_new will be automatically disabled if the configuration for the feed has changed since the last run.