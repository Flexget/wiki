= How to install !FlexGet =

If you're familiar with subversion I recommend getting checkout so you can update application more easily.

=== Checkout from SVN ===

{{{
svn co http://217.112.253.41/svn/flexget <path>
}}}

=== Update from SVN ===

Enter path where checkout and run

{{{
svn update
}}}

TODO: DOWNLOAD LOCATION

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
them by following instructions at library site in question.

= Running =

Running !FlexGet is easy, it's designed to be ran from user crontab (daemon mode later perhaps).

Install it into ~/flexget (or any path) and run:

{{{
crontab -e
}}}

Enter one new line on crontab:

{{{
*/30 * * * * ~/flexget/flexget.py -c <configuration file> -q
}}}

This will run !FlexGet every 30 minutes. It is not recommended to run it more frequently since it will cause load on RSS-feeds it checks.

You should [wiki:Configuration write configuration file] before installing !FlexGet in crontab.