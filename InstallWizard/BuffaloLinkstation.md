'''{{{This page needs updated to use python 2.6 or 2.7 (and preferably pip.) Please feel free to do so.}}}'''
= Python set-up =

Assuming you are using the IPKG package manager, you will first need to set up python by using:

{{{
ipkg install python
}}}

if you would now just go ahead, download the setuptools, you would run out of space on your small Linkstation - hence you will need to do the following:

{{{
ipkg install py25-setuptools
ipkg install py25-sqlalchemy
ipkg install py25-feedparser
ipkg install py25-yaml
}}}
''(please note: you can also use Python 2.6)''

= !FlexGet setup =

You now can use easy_install to install !FlexGet:

{{{
easy_install-2.5 flexget
}}}

If you get a 'No space left on device' error this is due to the fact that the /tmp directory is held in RAM. In this case use the following workaround:

{{{
mkdir /tmp2
export TEMP=/tmp2 easy_install-2.5 flexget
}}}

You can check your installation using

{{{
python /opt/local/bin/flexget -V
-1.0r<your version>
}}}

To call FlexGet directly you can go for:

{{{
python /opt/local/bin/flexget
}}}

You will need a configuration file, whereas the most simple version you find on the homepage and more complete versions in the cookbook, linked below.

= Cron job =

If you want FlexGet to automatically run e.g. every 45 minutes you can include the following in your crontab:

{{{
*/45 * * * * /opt/bin/python25 /opt/local/bin/flexget
}}}

if you are not sure how to work with crontab, here a little longer explanation:

{{{
crontab -e
<i> (for edit mode)
<enter new line from above>
<ESC>, <:>, <w>, <q>, <ENTER> (to save and close)
#so you basically would load edit the crontab file (crontab -e), hit i, insert the new line, hit ESC, :wq, done
}}}

For sample configurations, check out the [wiki:Cookbook Cookbook].