== Using the synocommunity package ==
The synocommunity repository [https://synocommunity.com/] includes a !FlexGet package. Follow the homepage instructions to add synocommunity to your NAS, and then install Python and !FlexGet through the web interface. The config file will be available at `/usr/local/flexget/var/config.yml`.

An alternative is to install with `easy_install` as detailed in the rest of this tutorial.

== Installing with easy_install ==


''These instruction were written from memory some time after successfully installing !FlexGet on a Synology DS210j. If any packages fail to install then check the output messages for missing dependencies, version numbers, etc, and install the required packages. If you install !FlexGet following these instructions then please correct any errors, add missing information and delete this paragraph.''

= Set up environment =

You will need to be logged into the Synology NAS as root to install packages.

== ipkg ==

The first step is to install ipkg, the Package Management System that will be used to install packages. Follow the instructions at:

[http://forum.synology.com/wiki/index.php/Overview_on_modifying_the_Synology_Server,_bootstrap,_ipkg_etc]

== Python ==

Install Python 2.6 by running:

{{{
ipkg install python26
}}}

== easy_install ==

Install the Python setuptools package. This includes `easy_install` which will be used to install Python packages/eggs. To install, run:
{{{
ipkg install py26-setuptools
}}}

== SQLite ==

!FlexGet requires SQLite to be installed. Run:

{{{
ipkg install sqlite
}}}

== Transmission ==

If you wish to use the Transmission !BitTorrent client (recommended) instead of the built-in client then follow the instructions at:

[http://forum.synology.com/wiki/index.php/Transmission_HowTo]

or

[http://synoblog.superzebulon.org/tag/synology/]

== tranmissionrpc == 

If you will be using Transmission, then install the transmissionrpc package by running:

{{{
easy_install transmissionrpc
}}}

if you get an error along the lines of
{{{
/opt/local/lib/python2.5/site-packages (in --site-dirs) does not exist
}}}
you have to edit distutils.cfg (located in /opt/lib/python2.6/distutils) to point to the correct path.

Note: If you are still having issues with the above error, a work-around is to install package "Python" (version 2.7.x) followed by FlexGet through the Synology web manager.
Afterwards, add '''/volume1/@appstore/flexget/env/bin/''' to your PATH in /root/.profile (or /etc/profile).
This should give you a working config of easy_install.

= Next =

[wiki:InstallWizard/SynologyNAS/FlexGet Install FlexGet]
