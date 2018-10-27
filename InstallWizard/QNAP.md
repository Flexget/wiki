**`This page needs updated to use python 2.7 and pip. Please feel free to do so.`**
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

1) Install the Python 2.7.12.1 package from the Qnap App Store

2) Log in to your NAS via ssh

3) Enter the command below

```
export PATH=/opt/QPython2/bin:$PATH
```
Check the correct version of Python is installed and active using
```
python --version
```
This should return
```
python 2.7.12.1
```
Install Pip using
```
curl https://bootstrap.pypa.io/get-pip.py -o get-pip.py
python get-pip.py
```
Install Flexget using
```
Pip install flexget
```


Create your config.yml file in the directory /opt/local/

Put an entry in your cron to lauch flexget every 10 mins