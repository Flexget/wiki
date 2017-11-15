FlexGet is designed to be executed from user crontab.


### Using systemd/timers

If your system is running with systemd you can directly configure it to run the command every hours as the current user with the following command:

```bash
systemd-run --on-active="1h" --uid=`id -u` --gid=`id -g` `which flexget` execute
```

This will prompt you for the root password (as system services require root to be configured) and then will let you know the name of the service. You can confirm it was scheduled by looking at the system.d scheduler with `systemctl list-timers`.

### Using Cron

#### Detemine full path to executable
To determine where FlexGet command resides run:

```
which flexget
```

Example output: `/usr/local/bin/flexget`. This may be different in your environment!


#### Edit crontab
FlexGet is meant to be executed from users own crontab, **not** from /etc/crontab (root). Although this is possible it is highly discouraged.

To change default editor for crontab, you can use command:

```
export EDITOR=nano
```

^You may wish to add this into your ~/.bashrc so it will be always the default editor^

To edit user crontab execute command (Note: [ubuntu](https://help.ubuntu.com/community/CronHowto#Enable%20User%20Level%20Cron)):

```
crontab -e
```

Enter one new line on crontab:

```
@hourly /usr/local/bin/flexget --cron execute
```

This will run FlexGet every hour. You may run it more frequently as well, but I wouldn't recommend going below 30 minutes since it will cause unnecessary load on RSS-feeds and pages you're subscribed to. Some feed providers even ban your IP if you request feed too often.

To run more often you may use crontab in form of:

```
*/30 * * * * /usr/local/bin/flexget --cron execute
```

Where 30 is the time between executions.

#### Verification
Once FlexGet runs successfully from crontab it will log this few times into the log file. The log file is located in same directory as your configuration file.

### Daemon Mode
With FlexGet running in [daemon mode](/Daemon) you can use the [scheduler](/Plugins/Daemon/scheduler) plugin to define when your tasks should be run inside the configuration file.

To start the daemon at system boot you would use:

```
@reboot /usr/local/bin/flexget daemon start -d
```

There are also some other methods available, listed [here](/Daemon/Startup).