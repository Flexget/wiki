= Only New =

This plugin causes all undecided entries to be rejected at the end of a feed execution. These entries will be automatically rejected by the remember_rejected plugin on all future executions of the feed.

This should not be needed on most feeds, and may cause problems in instances where processing an entry on the second run is desired (e.g. lookup was not available first run.) It is most helpful in cases where performance is an issue.

'''Example:'''

{{{
only_new: yes
}}}

You can allow old entries to be processed again by using the {{{--forget-rejected}}} option. In addition, rejections will be automatically forgotten if the configuration for the feed has changed since the last run.