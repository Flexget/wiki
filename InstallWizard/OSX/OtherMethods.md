# [Install Wizard](/InstallWizard) > [OSX](/InstallWizard/OSX) > Other Methods

## Other / Deprecated
### Installing with MacPorts and pip
*Unverified, but this should be the best way*

Install the Python pip module using MacPorts:

http://www.macports.org/ports.php?by=name&substr=py%25-pip

after that you should be able to install FlexGet simply with

```
py-pip install flexget
```

### Prior versions of macOS

*NOTE: Works on 10.6 and 10.7. It also works in 10.5, but after easy_install'ing flexget, you also need to install "simplejson" the same way.*

```
sudo easy_install flexget
```

Some plugins will require their own installs, e.g.:

```
sudo easy_install transmissionrpc
```

Some Yosemite (10.10) users have reported issues with easy_install. Using easy_install to install pip, then using pip to install setuptools and flexget has been reported to be successful:

```
sudo easy_install pip
sudo pip install setuptools
sudo pip install flexget
```

Pip can then be used for upgrades:

```
sudo pip install --upgrade setuptools
sudo pip install --upgrade flexget
```

When upgrading, it is best practice to unload the Launch Agent to avoid nasty errors.



### Other
 * OSX 10.5 uses python 2.5
 * OSX 10.6 uses python 2.6

Easy install tools needs to be compiled.
You can then use the InstallEggMac guide to get the dependencies, and install the egg.

 * [see old 0.9.x guide](/InstallOSX)
 * [Notes for 1.0 in mac 10.6](/InstallEggMac)

**Gathered from irc**

```
> aha!
> got it!
> :-)
> flexget with mac ports
> export PYTHONPATH=/opt/local/Library/Frameworks/Python.framework/Versions/2.6/lib/python2.6/site-packages
> woot
```

### Installing through Fink
[Fink](http://www.finkproject.org/) has FlexGet in unstable, as of 2010-07-24.  You should just need to run 'fink install flexget' with unstable enabled and it will install all dependencies.

## Continue
Once you've installed FlexGet, learn how to [autorun the daemon](/InstallWizard/OSX/Autorun).