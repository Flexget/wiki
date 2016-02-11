= Configuring `upstart` =

!FlexGet should be run in daemon mode. Starting with DSM 5.0, Upstart is available as part of the Synology OS and is the best way to manage system services.

== Modify `/etc/rc.optware` ==

You'll need to modify the file `/etc/rc.optware` so that your system tells Upstart when your optware (user-installed packages) has loaded. First, create a backup of the existing file in case something bad happens and you need to revert.

{{{
$ cp /etc/rc.optware /etc/rc.optware.bak
}}}

Using your editor of choice (`vi` is installed by default), open `/etc/rc.optware` for editing. Look for the following line:

{{{
mount -o bind ${REAL_OPT_DIR} /opt
}}}

Immediately after that line and at the same level of indentation, add the following line:

{{{
initctl emit optware-ready
}}}

== Transmission service script ==

If you're using Transmission as your !BitTorrent client, and you installed it according to the [wiki:InstallWizard/SynologyNAS previous instructions], you'll want to use `upstart` to manage the Transmission daemon. If you aren't using Transmission, skip this section.

It is highly recommended that you run the Transmission daemon as a non-root user. Use the Synology web UI to create a new user. This tutorial assumes this user is called `transmission`. The user you create will need write access to wherever you want your downloaded data to end up.

Next, you'll need to create an `upstart` script to manage the Transmission daemon. Create a file at `/etc/init/transmission-daemon.conf`. Its contents should look like this:

{{{
description "Transmission daemon"
author "YOUR NAME HERE"

start on optware-ready
stop on runlevel [06]

respawn
respawn limit 5 10

console log

expect fork

setuid transmission

exec /opt/bin/transmission-daemon
}}}

If your user is named something besides `transmission`, change the `setuid` line above to whatever name you used.

=== Configuring Transmission ===

Transmission creates its config files in the home directory of the user that starts the daemon, at `~/.config/transmission-daemon`. The `settings.json` file contained therein allows you to configure the daemon's options.

If you have never before run Transmission as the `transmission` user, you'll need to do so to create these config files. Having written the script above, you can use Upstart to control Transmission:

{{{
$ start transmission-daemon
}}}

Edits you make to Transmission's settings file will only stick if the daemon is not running while you edit the config file. So let it run for a few seconds and then stop it:

{{{
$ stop transmission-daemon
}}}

Open `~/.config/transmission-daemon/settings.json` for editing. A full list of options is available on the [https://trac.transmissionbt.com/wiki/EditConfigFiles Transmission Wiki]. In general you can configure Transmission however you want, but you will at least want to set `watch-dir` and change `watch-dir-enabled` to `true`. Unless you have reason to put it somewhere else, the `transmission` user's home directory is a fine place for the watch directory.

With a watch directory set up, having !FlexGet download torrents with Transmission is as simple as downloading the .torrent files to said directory.

== !FlexGet service script ==

Create an `upstart` script to manage the !FlexGet daemon. Create a file at `/etc/init/flexget-daemon.conf`. Its contents should look like this:

{{{
description "FlexGet daemon"
author "YOUR NAME HERE"

start on started transmission-daemon
stop on stopping transmission-daemon

respawn
respawn limit 5 10

console log

setuid transmission

exec /opt/local/bin/flexget daemon start

pre-stop exec /opt/local/bin/flexget daemon stop
}}}

If you are not using Transmission, change `start on started transmission-daemon` to `start on optware-ready` and change `stop on stopping transmission-daemon` to `stop on runlevel [06]`. You can also remove the `setuid transmission` line, but it is still recommended that you not run !FlexGet as the root user.

== Important caveat ==

Because Synology just can't help being a pain in the ass sometimes, the contents of `/etc/init` is reset to system defaults '''every time you install a major version OS update'''. So, when you update from e.g. DSM 5.1 to DSM 5.2, your `/etc/init/transmission-daemon.conf` and `/etc/init/flexget-daemon.conf` files will get wiped out. For this reason it is important that you back them up so that you can easily replace them after updating. Minor version updates do not reset `/etc/init`.

== That's all, folks ==

The setup above will automatically start !FlexGet (and optionally Transmission) in daemon mode whenever your Synology server boots up. Enjoy!