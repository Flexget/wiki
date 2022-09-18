---
title: BuffaloLinkstation
description: 
published: true
date: 2022-09-18T05:00:07.014Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:04.357Z
---

# Python set-up
Assuming you are using the IPKG package manager, you will first need to set up python by using:
```
ipkg install python27 py27-setuptools
easy_install-2.7 pip
```

You might want to remove old version of python25 (including py25* packages and /opt/local/lib/python2.5/ directory) before going any further.

# FlexGet setup
You now can use pip to install FlexGet:

```
/opt/local/bin/pip install flexget
```

If you get a 'No space left on device' error this is due to the fact that the /tmp directory is held in RAM. In this case use the following workaround:

```
mkdir /tmp2
export TEMP=/tmp2
/opt/local/bin/pip install flexget
```

You can check your installation using

```
/opt/local/bin/flexget --check
/opt/local/bin/flexget -V
```

To call FlexGet directly you can go for:

```
/opt/local/bin/flexget
```

You will need a configuration file, whereas the most simple version you find on the homepage and more complete versions in the cookbook, linked below.

# FlexGet upgrade
Run the following command:
```
/opt/local/bin/pip install --upgrade flexget
/opt/local/bin/flexget --check
```

Sometimes upgrading doesn't work, especially when you have multiple version of PHP installed. In that case you need to reinstall. Run the following to uninstall flexget (no worries, your settings stay where they are):
```
/opt/local/bin/pip uninstall flexget
```

After that make sure that the /opt/local/lib/python<version>/site-packages does not contain references to flexget anymore. Also make sure that your $TEMP folder doesn't contain any flexget references (delete them).

After deleting everything, just reinstall.

# Cron job
If you want FlexGet to automatically run e.g. every 45 minutes you can include the following in your crontab:

```
*/45 * * * * /opt/bin/python25 /opt/local/bin/flexget
```

if you are not sure how to work with crontab, here a little longer explanation:

```
crontab -e
<i> (for edit mode)
<enter new line from above>
<ESC>, <:>, <w>, <q>, <ENTER> (to save and close)
#so you basically would load edit the crontab file (crontab -e), hit i, insert the new line, hit ESC, :wq, done
```

For sample configurations, check out the [Cookbook](/Cookbook).