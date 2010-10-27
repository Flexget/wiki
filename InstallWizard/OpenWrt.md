OpenWrt is described as a Linux distribution for embedded devices.

= Set up environment =

== Python ==

Python, !FlexGet and dependencies need ~7mb of free space:

{{{
opkg install python
opkg install python-sqlite3
}}}

== easy_install ==

{{{
opkg install distribute
}}}

Beware of this ticket: https://dev.openwrt.org/ticket/8135

== Install ==

Run command:

{{{
python /usr/lib/python2.6/site-packages/easy_install.py http://download.flexget.com/unstable/FlexGet-1.0rXXXX-py2.6.egg
}}}

This will install !FlexGet and all additional components it requires.

== Verify installation ==

Run command:

{{{
# flexget -V
FlexGet 1.0r1565
}}}

=== Notes ===

I needed to disable prowl:
{{{
mv /usr/lib/python2.6/site-packages/FlexGet-1.0r1565-py2.6.egg/flexget/plugins/output_prowl* /tmp
}}}

dependencies which will be installed with easy_install:

{{{
progressbar-2.3
pynzb-0.1.0
PyRSS2Gen-1.0.0
html5lib-0.90
BeautifulSoup-3.1.0.1
PyYAML-3.09
SQLAlchemy-0.6.5
feedparser-4.1
}}}

