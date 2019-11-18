# [Install Wizard](/InstallWizard) > [SynologyNAS](/InstallWizard/SynologyNAS) > PythonPackage

## Caveats

<div class="alert alert-warning" role="alert">
  FlexGet supports Python 3.6-3.8
</div>

This method uses the Python installation available in DSM's Package Center. As such, it will only work while the version of Python available there is one of those listed above. At time of writing, the DSM package provides Python 3.5.1.

## Install Python

Go to the DSM Package Center and install the Python 3 package.

## Install FlexGet

Before proceeding any further, you'll want to make sure that whatever location `pip` installs to is in your `PATH` so that you can access `flexget` easily.

Install using the following command:

```
pip3 install flexget
```

## Verify installation
Run the following command, and FlexGet will display its version number:

```
$ flexget --version
2.3.42
You are on the latest release.
```

## Configuration
Before you can run FlexGet you must must [write a configuration file](/Configuration) and test that it works correctly. FlexGet stores a number of files in the same directory as its config file so make sure the user that will be executing FlexGet can write to the appropriate path.

## Configuring Upstart
Starting with DSM 5.0, Upstart is available as part of the Synology OS and is the best way to manage system services. You want to run FlexGet in daemon mode, and we'll use Upstart to make sure the daemon starts up and shuts down when it should.

### Modify `/etc/rc.local`
We're going to modify the file `/etc/rc.local` (which you created as part of installing `opkg`) so that your system tells Upstart when your packages have been loaded. Using your editor of choice (`vi` is installed by default), open `/etc/rc.local` for editing. At the end of the file, add the following line:

```
initctl emit opt-ready
```

### FlexGet service script
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

# Important caveat
Because Synology just can't help being a pain in the ass sometimes, the contents of `/etc/init` is reset to system defaults **every time you install a major version OS update**. So, when you update from e.g. DSM 5.1 to DSM 5.2, your `/etc/init/transmission-daemon.conf` and `/etc/init/flexget.conf` files will get wiped out. For this reason it is important that you back them up so that you can easily replace them after updating. Minor version updates do not reset `/etc/init`.

## That's all, folks
The setup above will automatically start FlexGet in daemon mode whenever your Synology server boots up. Enjoy!