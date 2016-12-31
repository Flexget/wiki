# Configuring Upstart
Starting with DSM 5.0, Upstart is available as part of the Synology OS and is the best way to manage system services. You want to run FlexGet in daemon mode, and we'll use Upstart to make sure the daemon starts up and shuts down when it should.

## Modify `/etc/rc.local`
We're going to modify the file `/etc/rc.local` (which you created as part of installing `opkg`) so that your system tells Upstart when your packages have been loaded. Using your editor of choice (`vi` is installed by default), open `/etc/rc.local` for editing. At the end of the file, add the following line:

```
initctl emit opt-ready
```

## Transmission service script
If you're not using Transmission, skip this section.

If you're using Transmission as your BitTorrent client, and you installed it according to the [previous instructions](/InstallWizard/SynologyNAS), then Transmission is actually already set up to run where your system starts. Installing the Transmission package created a script at `/opt/etc/init.d/S88transmission` which will be executed by on boot. For many people, this is fine. But if you're like me and you don't mind tinkering, using Upstart to manage the Transmission daemon will give you more detailed control over how it runs (e.g., let you run the daemon as a non-root user). If you don't want to tinker, skip this section.

It is highly recommended that you run the Transmission daemon as a non-root user. Use the Synology web UI to create a new user. This tutorial assumes this user is called `downloader`. The user you create will need write access to wherever you want your downloaded data to end up.

Since we're going to be using Upstart to manage the Transmission daemon, we don't want the default init script to be run as well (or you'll end up with two daemon processes running). You can either delete `/opt/etc/init.d/S88transmission` (but be warned that upgrading the Transmission package will replace this file), or simply remove the line in `/etc/rc.local` that triggers the init scripts and manage everything with Upstart. If you want to do the latter, remove the following line from `/etc/rc.local`:

```
/opt/etc/init.d/rc.unslung start
```

Next, you'll need to create an Upstart script to manage the Transmission daemon. Create a file at `/etc/init/transmission-daemon.conf`. Its contents should look like this:

```
description "Transmission"
author "YOUR NAME"

start on opt-ready
stop on runlevel [06]

respawn
respawn limit 5 10

console log

expect fork

setuid downloader

env TRANSMISSION_WEB_HOME=/opt/share/transmission/web
exec /opt/bin/transmission-daemon
```

If your user is named something besides `downloader`, change the `setuid` line above to whatever name you used.

### Configuring Transmission
Transmission creates its config files in the home directory of the user that starts the daemon, at `~/.config/transmission-daemon`. The `settings.json` file contained therein allows you to configure the daemon's options.

If you have never before run Transmission as the `downloader` user, you'll need to do so to create these config files. Having written the script above, you can use Upstart to control Transmission:

```
$ start transmission-daemon
```

Edits you make to Transmission's settings file will only stick if the daemon is not running while you edit the config file. So let it run for a few seconds and then stop it:

```
$ stop transmission-daemon
```

Open `~/.config/transmission-daemon/settings.json` for editing. A full list of options is available on the [Transmission Wiki](https://trac.transmissionbt.com/wiki/EditConfigFiles). In general you can configure Transmission however you want, but you will at least want to set `watch-dir` and change `watch-dir-enabled` to `true`. Unless you have reason to put it somewhere else, the `downloader` user's home directory is a fine place for the watch directory.

With a watch directory set up, having FlexGet download torrents with Transmission is as simple as downloading the .torrent files to said directory.

## FlexGet service script
Create an Upstart script to manage the FlexGet daemon at `/etc/init/flexget.conf`. Its contents should look like this:

```
description "FlexGet"
author "YOUR NAME"

start on opt-ready
stop on runlevel [06]

respawn
respawn limit 5 10

console log

setuid downloader

exec /opt/bin/flexget daemon start

pre-stop exec /opt/bin/flexget daemon stop
```

As with Transmission, it is not recommended to run FlexGet as the root user.

## Important caveat
Because Synology just can't help being a pain in the ass sometimes, the contents of `/etc/init` is reset to system defaults **every time you install a major version OS update**. So, when you update from e.g. DSM 5.1 to DSM 5.2, your `/etc/init/transmission-daemon.conf` and `/etc/init/flexget.conf` files will get wiped out. For this reason it is important that you back them up so that you can easily replace them after updating. Minor version updates do not reset `/etc/init`.

## That's all, folks
The setup above will automatically start FlexGet (and optionally Transmission) in daemon mode whenever your Synology server boots up. Enjoy!