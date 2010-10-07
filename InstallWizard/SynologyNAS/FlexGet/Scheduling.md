= Scheduling =

=== Edit crontab ===

!FlexGet is meant to be executed the from a user's own crontab, '''not''' from /etc/crontab (root). Although this is possible it is highly discouraged. 

See [http://forum.synology.com/enu/viewtopic.php?f=39&t=13473] for details of how to setup scheduling for users other than root.

Add a new user, crontab. As root, create a file named 'crontab' in crontab's home directory containing:
{{{
@hourly crontab /path/to/flexget --cron
}}}

This will run !FlexGet every hour. You may run it more frequently as well, but I wouldn't recommend going below 30 minutes since it will cause an unnecessary load on RSS feeds and pages you're subscribed to. Some feed providers even ban your IP if you request a feed too often.

To run more often you may use crontab like this:

{{{
*/30 * * * * crontab /path/to/flexget --cron
}}}

Where 30 is the number of minutes between executions.

Add the crontab to /usr/syno/etc/rc.d/S04crond.sh as described in the link above.

To start or stop cron, use the commands:
{{{
/usr/syno/etc.defaults/rc.d/S04crond.sh start
/usr/syno/etc.defaults/rc.d/S04crond.sh stop 
}}}

Note that cron will need to be restarted after making changes to a crontab.
