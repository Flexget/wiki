---
title: AutoUpgrade
description: 
published: true
date: 2022-09-18T05:19:29.422Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:19:26.849Z
---

# Bash Script for automatically updating Flexget
This bash script is for safely automating upgrading of flexget.  It checks the config after upgrade and reverts to the previous version if the config check fails, this way flexget continues to run until the user can update the config and upgrade flexget manually


The below script is intended as an example, it is designed to be run on linux as root with cron daily or weekly.  Customization for your own environment is recommened, please make sure to at least set the variables for FLEXGET_USER and CONFIG_PATH


Details: The script first checks if a new version of Flexget is avalaible.  If there is, the flexget service is stopped and the cron jobs for the flexget user are temporarliy disabled, the script waits for all instances of flexget to exit and kill the processes if they do not.  It then automatically upgrades flexget with using pip.  Once the upgrade is complete, the script finds all files named “config.yml” and runs “flexget check” for each file.  If the check should fail for any of the files due to changes in the flexget code, flexget is uninstalled by pip and the version of flexget that was previously installed is installed again.  Finally, the cron jobs are restored and the flexget service is started.

```
#!/bin/bash
FLEXGET_USER=flexget
CONFIG_PATH=/home/flexget/

FUPDATE=$(/usr/local/bin/flexget -V)
if (echo $FUPDATE | grep "You are on the") > /dev/null; then
        echo "Already on the latest version"
	exit
else
	echo Flexget Upgrade Available
	echo $FUPDATE
fi

CURVER=$(/usr/local/bin/flexget -V | sed -n '1p')
FAILED=0
echo Disabling Cron Jobs
sudo -u $FLEXGET_USER crontab -l > $CONFIG_PATH/cron_backup.txt
sudo -u $FLEXGET_USER crontab -r
echo Stoping Services
/usr/sbin/service flexget stop
sleep 10

PSCOUNT=$(ps -f -u $FLEXGET_USER --no-headers | grep -c flexget)
if [ $PSCOUNT -ne 0 ]; then
	sleep 10
	PSCOUNT=$(ps -f -u $FLEXGET_USER --no-headers | grep -c flexget)
fi
if [ $PSCOUNT -ne 0 ]; then
        sleep 10
        PSCOUNT=$(ps -f -u $FLEXGET_USER --no-headers | grep -c flexget)
fi
if [ $PSCOUNT -ne 0 ]; then
        sleep 10
	echo Sending PKill
        pkill -u $FLEXGET_USER
fi

# Install Flexget Upgrade
echo Installing Flexget Upgrade
/usr/local/bin/pip install --upgrade -q flexget
sleep 5

(find -L $CONFIG_PATH -name config.yml 2>/dev/null) |
while read filename
do
    config=${filename/$CONFIG_PATH/}
    echo Checking "***" ${config/\/config.yml/}
    sudo -u $FLEXGET_USER /usr/local/bin/flexget -c $filename check
    if [ $? -ne 0 ]; then
        FAILED=$((FAILED+1))
    fi
done

if [ $FAILED -ne 0 ]; then
	echo Flexget Check Failed on $FAILED Config Files
	echo Removing Flexget
	yes | /usr/local/bin/pip uninstall -q flexget
	sleep 5
	printf "\n"
	echo Installing Flexget Version $CURVER
	/usr/local/bin/pip install -q flexget==$CURVER
	sleep 5
else
	echo All Flexget Checks Passed
fi

echo Restore Cron Jobs
sudo -u $FLEXGET_USER crontab $CONFIG_PATH/cron_backup.txt
echo Starting Services
/usr/sbin/service flexget start
echo Complete
/usr/local/bin/flexget -V
```