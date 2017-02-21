# Automatic Daemon Startup


## Linux
There are several methods which can be used to start the daemon on linux.

### Cron
The easiest method is probably to have cron start the daemon on boot, and is compatible with most (all?) flavors of linux.

To edit user crontab execute command (Note: [ubuntu](https://help.ubuntu.com/community/CronHowto#Enable%20User%20Level%20Cron)):

```
crontab -e
```

And add the line:

```
@reboot /usr/local/bin/flexget daemon start -d
```

### Upstart script (Ubuntu family)
To have flexget daemon automatically start on system boot

sudo vim /etc/init/flexget.conf
```/bin/bash
# Flexget daemon autostart                                                                                                                                                      

description "Flexget daemon"
author "Kempe / Shrike"

start on (filesystem and networking) or runlevel [2345](/2345)
stop on runlevel [016](/016)

respawn
respawn limit 5 30

# Will not respawn if flexget daemon is stopped or killed/terminated
normal exit 0 TERM

env user=<YOURUSERNAME>
# to find your local run the locale command an example local would be en_US.utf8
env LANG=<YOUR UTF-8 LOCALE>
#log levels none, critical,error, warning, info, verbose, debug, trace
env loglvl=info

exec start-stop-daemon -S --chuid $user --user $user --exec /usr/local/bin/flexget -- --loglevel $loglvl daemon start
```

Read log: 
```
sudo tail -f /var/log/upstart/flexget.log
```

Control daemon:

```
sudo status flexget
sudo stop flexget
sudo start flexget
```

### Insserv script (Debian compatible)
This script allows the flexget daemon to automatically start on system boot.

All of the following should be done as the root user.

First, create a /etc/default/flexget file with the following content :

```
# Configuration for /etc/init.d/flexget

# User to run flexget as.
# Daemon will not start if left empty.
FGUSER=""

# Full path to the flexget config.yml file to use.
# Defaults to FGUSER $HOME/.flexget/config.yml
CONFIG=""

# Path to the directory where flexget should log. Do not add trailing slash.
# Defaults to the FGUSER $HOME/.flexget directory
LOG=""

# Log verbosity 
# Available options : none critical error warning info verbose debug trace
# Defaults to info
LEVEL=""
```

Please note that FGUSER needs to be defined for the daemon to start. It can be set to your current user, or you can run flexget as its own user.

Then, create the /etc/init.d/flexget file :

```/bin/bash
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
        log_action_msg "$DESC: Could not find flexget executable. Exiting."
        exit 2
fi

# Read configuration variables
if [ -r /etc/default/$NAME ]; then
        . /etc/default/$NAME
else
        log_action_msg "$DESC: /etc/default/$NAME not found. Exiting."
        exit 2
fi

# Exit if FGUSER has not been set in /etc/default/flexget
if [ -z $FGUSER ]; then
        log_action_msg "$DESC: FGUSER not set in /etc/default/$NAME. Exiting."
        exit 2
fi

# Function to verify if flexget is already running
run_check() {
        if [ -e $PIDFILE ]; then
               status_of_proc -p $PIDFILE $DAEMON $NAME > /dev/null && RETVAL=0 || RETVAL="$?"
        else
                RETVAL="2"
        fi
}

end_log() {
        if [ $RETVAL -eq 0 ]; then
                log_end_msg 0
                return 0
        else
                log_end_msg 1
                exit 1
        fi
}

# Function to define config file, log file and log level
conf_check() {
        if [ -z "$CONFIG" ]; then
                OPTIONS="$OPTIONS"
        else
                OPTIONS="-c $CONFIG"
        fi
        if [ -z "$LOG" ]; then
                OPTIONS="$OPTIONS"
        else
                OPTIONS="$OPTIONS -l $LOG/flexget.log"
                if [ ! -d "$LOG" ]; then 
                        mkdir -p -m 750 $LOG
                        chown $FGUSER $LOG
                fi
        fi

        if [ -z $LEVEL ]; then
                OPTIONS="$OPTIONS"
        else
                OPTIONS="$OPTIONS -L $LEVEL"
        fi
}

start_flexget() {
        run_check
        if [ $RETVAL = 0 ]; then
                log_action_msg "$DESC: Already running with PID $(cat $PIDFILE). Aborting."
                exit 2
        else
                conf_check
                log_daemon_msg "$DESC: Starting the daemon."
                start-stop-daemon --start --background --quiet --pidfile $PIDFILE --make-pidfile --chuid $FGUSER \
                --user $FGUSER --exec $DAEMON -- $OPTIONS daemon start
                RETVAL=$?
                end_log
        fi
}

stop_flexget() {
        run_check
        if [ $RETVAL = 0 ]; then
                log_daemon_msg "$DESC: Stopping the daemon."
                start-stop-daemon --stop --quiet --chuid "$FGUSER" --pidfile "$PIDFILE" --retry 30
                RETVAL=$?
                [ -e "$PIDFILE" ] && rm -f "$PIDFILE"
                end_log
        else
                log_action_msg "$DESC: Not currently running. Aborting."
                exit 2
        fi
}

status_flexget() {
        run_check
        if [ $RETVAL = 0 ]; then
                log_action_msg "$DESC: Currently running with PID $(cat $PIDFILE)."
        else
                log_action_msg "$DESC: Not currently running."
        fi
        exit $RETVAL
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
```

Then, give executions rights to the script :

```
chmod +x /etc/init.d/flexget
```

And then, generate the necessary symlinks for the service to start on boot :
```
insserv -d flexget

OR

update-rc.d flexget defaults
```

To start, stop or check if the daemon is running :
```
/etc/init.d/flexget start
/etc/init.d/flexget stop
/etc/init.d/flexget status

OR

service flexget start
service flexget stop
service flexget status
```
### Systemd system unit (Arch Linux, Fedora, etc.)
To have flexget run as a system unit.

```
[Unit](/Unit)
Description=Flexget Daemon
After=network.target

[Service](/Service)
Type=simple
User=daemon
Group=daemon
UMask=000
WorkingDirectory=/etc/flexget
ExecStart=/usr/bin/flexget daemon start
ExecStop=/usr/bin/flexget daemon stop
ExecReload=/usr/bin/flexget daemon reload

[Install](/Install)
WantedBy=multi-user.target
```

The above assumes that there is a daemon user and group available. Modify as needed.

Now, create the location to store flexgets configuration file, logs and database.

```
sudo mkdir /etc/flexget
sudo chown daemon:daemon /etc/flexget
```

You can now place your config.yml file in the /etc/flexget directory.

Enable or disable Flexget at boot using :

```
sudo systemctl enable flexget
sudo systemctl disable flexget
```

Read the systemd log: 

```
journalctl -u flexget
```

Control the daemon:

```
systemctl status flexget
systemctl stop flexget
systemctl start flexget
```


### Systemd user unit (Arch Linux, Fedora, etc)
From @mkaito, Trac #[2526](https://flexget.com/ticket/2526).

To have flexget by accessible as a systemd user unit.

See [here](https://wiki.archlinux.org/index.php/Systemd/User#User_Services) for more.

sudo vim /usr/lib/systemd/user/flexget.service or vim ~/.config/systemd/user/flexget.service
```
[Unit](/Unit)
Description=FlexGet Daemon
After=network.target

[Service](/Service)
ExecStart=/usr/bin/flexget daemon start
ExecStop=/usr/bin/flexget daemon stop
ExecReload=/usr/bin/flexget daemon reload

[Install](/Install)
WantedBy=default.target
```

Allows users who are not logged in to run long-running services.
A user manager is spawned for the user at boot and kept around after logouts.
```
sudo loginctl enable-linger <username>
```

Any end-users can enable or disable it using :
```
systemctl --user enable flexget
systemctl --user disable flexget
```

Read log: 
```
journalctl --user --user-unit flexget
```

Control daemon:

```
systemctl --user status flexget
systemctl --user stop flexget
systemctl --user start flexget
```


## As a Windows Scheduled Task
In the Task Scheduler, "Create a Task". Use a descriptive name. Set a new trigger - "At log on" or "At startup" are good candidates. Optionally set a small delay. Configure an action - "Start a program". Navigate to your Python scripts folder and select "flexget-headless.exe". Add arguments: "daemon start". Hit "OK". Optionally run your new task, then check on it using flexget daemon status.

## As an OS X Launch Agent
Do not use this method if you want to set up Flexget to run at an interval as described [here](/InstallWizard/OSX#Autorun). If you have set up the Launch Agent described in the OS X install section, replace it's plist with the one described below.

This method additionally overcomes the issues associated with launching the daemon in the background on OS X, allowing it to run in the background without an open Terminal window.

Create /Users/USERNAME/Library/LaunchAgents/com.flexget.plist with:

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>Label</key>
	<string>com.flexget</string>
	<key>ProgramArguments</key>
	<array>
		<string>/usr/local/bin/flexget</string>
		<string>daemon</string>
		<string>start</string>
	</array>
	<key>Nice</key>
	<integer>1</integer>
	<key>RunAtLoad</key>
	<true/>
</dict>
</plist>
```

**Note**: On some systems, FlexGet installs itself into `/bin/flexget` instead of `/usr/local/bin/flexget`; type `which flexget` to find out where the FlexGet binary is located and modify `com.flexget.plist` accordingly.