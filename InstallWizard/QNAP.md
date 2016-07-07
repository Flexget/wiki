**`This page needs updated to use python 2.6 or 2.7 (and preferably pip.) Please feel free to do so.`**
# TODO: write
```
ipkg install py25-setuptools
easy_install flexget
```

This should work, but for some it doesn't.

If you're low on disk space on root try [subversion route](/Subversion).

See forum thread [here](http://forum.qnap.com/viewtopic.php?f=16&t=24864)

On some systems the /tmp folder is not big enough to allow the installation to complete. You can temporarily make it bigger by executing:
```
mount -oremount,size=128M /tmp
```

# NO8080: write
For Python 2.7 on QNAP perform the following steps,

1) Install the QNAP Optware QPKG from the web GUI

2) Log in to your NAS via ssh

3) Enter the commands

```
ipkg install python27
ipkg install py27-setuptools
easy_install-2.7 flexget
```

If you want to use Transmission then enter the command
```
easy_install-2.7 transmissionrpc
```

To test it is working use the command
```
python2.7 /opt/local/bin/flexget -V
```

Create your config.yml file in the directory /opt/local/

Put an entry in your cron to lauch flexget every 10 mins