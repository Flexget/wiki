= How to install !FlexGet =

== Download ==

[http://download.flexget.com Download packages from here]

== Checkout from SVN ==

If you're familiar with subversion and want to stay in bleeding edge you can checkout directly from development repository.

{{{
svn co http://svn.flexget.com/trunk <path>
}}}

=== Update from SVN ===

Enter path where you did checkout and run

{{{
svn update
}}}


== Depencies ==

!FlexGet depens on single external library on Python2.3 or later. Without this you cannot run application.

* [http://pyyaml.org/ PyYAML]

Optionally if you wish to access html pages you'll need:

* [http://www.crummy.com/software/BeautifulSoup/ BeautifulSoup]

And if you want to access RSS feeds you'll need:

* [http://www.feedparser.org/ feedparser]

On Debian and Ubuntu you can use apt-get to install these:

{{{
sudo apt-get install python-yaml python-beautifulsoup python-feedparser
}}}

If you are running other distribution check it's package management. If it does not have these packages available you can still install 
them manually by following instructions at library site in question. Or you could use the [http://peak.telecommunity.com/DevCenter/EasyInstall Easy Install] Python installation module. [http://pyyaml.org/ PyYAML], [http://www.crummy.com/software/BeautifulSoup/ BeautifulSoup] and [http://www.feedparser.org/ feedparser] are available.

= Upgrading =

!FlexGet is currently under constant change so upgrading may cause problems. 

Safest way to upgrade is to run your old version normally once, then update to new version and run application with --reset parameter. This will reset session and learn all current matches as already downloaded items.

= Running =

Running !FlexGet should be easy, it's designed to be executed from user crontab (daemon mode later perhaps).

Install it into ~/flexget (or any path) and run:

{{{
crontab -e
}}}

Enter one new line on crontab:

{{{
@hourly ~/flexget/flexget.py -q
}}}

This will run !FlexGet every hour. You may run it more frequently as well, but I wouldn't recommend going below 30 minutes since it will cause unnecessary load on RSS-feeds and pages you're subscribed to.

You should [wiki:Configuration write configuration file] before installing !FlexGet in crontab.

== Manual execution ==

!FlexGet can be tested by executing it manually. See [wiki:Parameters parameters].

''TODO: Improve this section''