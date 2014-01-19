= Daemon =

!FlexGet can be run in daemon mode, which means it will always run in the background, periodically running tasks on a schedule, or running the tasks initiated by another instance of !FlexGet.

To launch the !FlexGet daemon, use the `start` command:
[[BR]]
^''Note: Using the optional `-d` switch will send the !FlexGet daemon to the background.''^
{{{
flexget daemon start [-d]
}}}


To stop a currently running daemon you can use `stop`:
{{{
flexget daemon stop
}}}
To check the status of the flexget daemon you can use `status`:
{{{
flexget daemon status
}}}
To restart the flexget daemon you can use `restart`: (Not yet implemented)
{{{
flexget daemon restart
}}}

== Scheduling ==

To tell !FlexGet how often it should execute your tasks, you can set up the `schedules` block in the config file. Each schedule consists of a list of tasks to run, and an interval which they should be run at. When specifying tasks, wildcards such as `*` (any characters), or `?` (any single character) can be used. If you run the daemon without specifying a schedules block, a default schedule of Every task, every hour is assumed. The configuration format is as follows:
{{{
schedules:
  - tasks: [list, of, tasks]
    interval:
      <weeks|days|hours|minutes>: <#>
      on_day: <monday|tuesday...>
      at_time: HH:MM [am|pm]  # 24h time can also be used
}}}
The `at_time` option can only be used when the interval is `days` or larger, and the `on_day` option can only be used when the interval is `weeks`. When only running a single task, the list notation need not be used. Here are some examples:
{{{
schedules:
  # Run every task once an hour
  - tasks: '*'
    interval:
      hours: 1
  # Run task_a and task_b every 30 minutes
  - tasks: [task_a, task_b]
    interval:
      minutes: 30
  # Run any task starting with 'weekly_' on tuesdays at 1 pm
  - tasks: 'weekly_*'
    interval:
      weeks: 1
      on_day: tuesday
      at_time: 1:00 pm
}}}

If you would like to run the daemon without any builtin schedules, (perhaps you are still sending executions from cron, or some other source,) you can configure it with an empty list, like so:
{{{
schedules: []
}}}

'''Please Note:''' You may see a warning like the following when using schedules, for now you can safely ignore it.
{{{
2014-01-07 10:28 WARNING  manager                       Config line 11 is likely missing ':' at the end
}}}

== Remote Execution ==
If you run `flexget execute` while a daemon is running, the execution will be sent to the running daemon, and either run immediately, or queued for execution after the current running task has finished. The log results of this execution will be sent back to the calling terminal for viewing as well. This means that if you are running a daemon, you need not worry about concurrent calls of `flexget execute` having problems due to the lock file.

== Upstart script (Ubuntu family) ==
To have flexget daemon automatically start on system boot

sudo vim /etc/init/flexget.conf
{{{
# Flexget daemon autostart                                                                                                                                                      

description "Flexget daemon"
author "Kempe"

start on (filesystem and networking) or runlevel [2345]
stop on runlevel [016]

respawn
respawn limit 5 30

env uid=<USER_TO_RUN_AS>
env gid=<GROUP_TO_RUN_AS>

exec start-stop-daemon -S -c $uid:$gid -x /usr/local/bin/flexget -- daemon start
}}}

Read log: 
{{{ 
sudo tail -f /var/log/upstart/flexget.log
}}}

Control daemon:

{{{
sudo status flexget
sudo stop flexget
sudo start flexget
}}}

== Insserv script (Debian compatible) ==
This script allows the flexget daemon to automatically start on system boot.

All of the following should be done as the root user.

First, create a /etc/default/flexget file with the following content :

{{{
# Configuration for /etc/init.d/flexget

# User to run flexget as.
# Daemon will not start if left empty.
FGUSER=""

# Full path to the flexget config.yml file to use.
# Defaults to the FGUSER $HOME/.flexget/config.yml
CONFIG=""

# Path to the directory where flexget should log. Do not add trailing slash.
# Defaults to /home/$FGUSER/.flexget
LOG=""

# Log verbosity 
# Available options : none critical error warning info verbose debug trace
# Defaults to info
LEVEL=""
}}}

Please note that FGUSER needs to be defined for the daemon to start. It can be set to your current user, or you can run flexget as its own user.

Then, create the /etc/init.d/flexget file :

{{{
#!/bin/bash

### BEGIN INIT INFO
# Provides:          flexget
# Required-Start:    $network $remote_fs
# Required-Stop:     $network $remote_fs
# Should-Start:      
# Should-Stop:       
# Default-Start:     2 3 4 5
# Default-Stop:      0 1 6
# Short-Description: Flexget
# Description:       FlexGet is a multipurpose automation tool 
#                    for content like torrents, nzbs, podcasts,
#                    comics, series, movies, etc.
### END INIT INFO

# Author: Antoine Joubert, 19/01/2014

NAME="flexget"
DAEMON="/usr/local/bin/flexget"
SETTINGS="/etc/default/$NAME"

DESC="Flexget"
PIDFILE="/var/run/$NAME.pid"

set -e

. /lib/lsb/init-functions

unset FGUSER CONFIG LOG LEVEL

# Exit if flexget not installed
if [ ! -x "$DAEMON" ]; then
        echo "$DESC: Could not find flexget executable. Exiting."
        exit 2
fi

# Read configuration variables
if [ -r /etc/default/$NAME ]; then
        . /etc/default/$NAME
else
        echo "$DESC: /etc/default/$NAME not found. Exiting."
        exit 2
fi

# Exit if FGUSER has not been set in /etc/default/flexget
if [ -z $FGUSER ]; then
        echo "$DESC: FGUSER not set in /etc/default/$NAME. Exiting."
        exit 2
fi

# Function to verify if flexget is already running
run_check()
{
        if [ -e $PIDFILE ]; then
               status_of_proc -p $PIDFILE $DAEMON $NAME > /dev/null && RETVAL=0 || RETVAL="$?"
        else
                RETVAL="2"
        fi
}

# Function to define config file, log file and log level
conf_check() {
        if [ -z $CONFIG ]; then
                CONFIGFILE=""
        else
                CONFIGFILE="-c $CONFIG"
        fi

        if [ -z $LOG ]; then
                LOGFILE=""
        else
                LOGFILE="-l $LOG/flexget.log"
                if [ ! -d $LOG ]; then 
                        mkdir -p -m 750 $LOG
                fi
                chown $FGUSER $LOG
        fi

        if [ -z $LEVEL ]; then
                LOGLEVEL=""
        else
                LOGLEVEL="-L $LEVEL"
        fi
}

start_flexget() {
        run_check
        if [ $RETVAL = 0 ]; then
                echo "$DESC: Already running with PID $(cat $PIDFILE). Aborting."
                exit 2
        else
                conf_check
                log_daemon_msg "$DESC: Starting the daemon."
                if start-stop-daemon --start --background --quiet --pidfile $PIDFILE --make-pidfile --chuid $FGUSER \
                --user $FGUSER --exec $DAEMON -- $CONFIGFILE $LOGFILE $LOGLEVEL daemon start; then
                        log_end_msg 0
                else
                        log_end_msg 1
                fi
        fi
}

stop_flexget() {
        run_check
        if [ $RETVAL = 0 ]; then
                log_daemon_msg "$DESC: Stopping the daemon."
                if start-stop-daemon --stop --quiet --chuid "$FGUSER" --pidfile "$PIDFILE" --retry 30; then 
                        [ -e "$PIDFILE" ] && rm -f "$PIDFILE"
                        log_end_msg 0
                else
                        log_end_msg 1
                fi
        else
                echo "$DESC: Not currently running. Aborting."
        fi
}

status_flexget() {
        run_check
        if [ $RETVAL = 0 ]; then
                echo "$DESC: Currently running with PID $(cat $PIDFILE)."
        else
                echo "$DESC: Not currently running."
        fi
}

case "$1" in
        start)
                start_flexget
        ;;
        stop)
                stop_flexget
        ;;
        restart)
                stop_flexget && sleep 2 && start_flexget
        ;;
        status)
                status_flexget
        ;;
        *)
                echo "Usage: $0 {start|stop|restart|status}"
esac

exit 0
}}}

Then, give executions rights to the script :

{{{
chmod +x /etc/init.d/flexget
}}}

And then, generate the necessary symlinks for the service to start on boot :
{{{
insserv -d flexget

OR

update-rc.d flexget defaults
}}}

To start, stop or check if the daemon is running :
{{{
/etc/init.d/flexget start
/etc/init.d/flexget stop
/etc/init.d/flexget status

OR

service flexget start
service flexget stop
service flexget status
}}}