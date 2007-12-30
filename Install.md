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

!FlexGet depens on single external library on Python2.3 or later.

* [http://pyyaml.org/ PyYAML]

Optionally if you wish to use modules that process html pages you'll need

* [http://www.crummy.com/software/BeautifulSoup/ BeautifulSoup]

On debian based linux distros you can use apt-get to install these:

{{{
sudo apt-get install python-yaml python-beautifulsoup
}}}

If your distribution does not gave these packages available you can still install them by following instructions from library site.

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