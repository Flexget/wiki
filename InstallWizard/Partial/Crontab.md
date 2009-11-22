= Scheduling =

Before scheduling !FlexGet you must must [wiki:Configuration write a configuration file] and test that it works correctly.

!FlexGet is designed to be executed from user crontab (daemon mode later perhaps).

To change default editor for crontab, you can use command:

{{{
export EDITOR=nano
}}}

^You may wish to add this into your ~/.bashrc so it will be always the default editor^

To edit user crontab execute command (Note: [https://help.ubuntu.com/community/CronHowto#Enable%20User%20Level%20Cron ubuntu]):

{{{
crontab -e
}}}

Enter one new line on crontab:

{{{
@hourly flexget --cron
}}}

This will run !FlexGet every hour. You may run it more frequently as well, but I wouldn't recommend going below 30 minutes since it will cause unnecessary load on RSS-feeds and pages you're subscribed to. Some feed providers even ban your IP if you request feed too often.

To run more often you may use crontab in form of:

{{{
*/30 * * * * ~/flexget/flexget.py -q
}}}

Where 30 is the time between executions.