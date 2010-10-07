= Set up environment =

''These instruction were written from memory some time after successfully installing !Flexget on a Synology DS210j. If any packages fail to install then check the output messages for missing dependencies, version numbers, etc, and install the required packages. If you install !Flexget following these instructions then please correct any errors, add missing information and delete this paragraph.''

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

!Flexget requires SQLite to be installed. Run:

{{{
ipkg install sqlite
}}}

== Transmission ==

If you wish to use the Transmission BitTorrent client (recommended) instead of the built-in client then follow the instructions at:

{{{
[http://forum.synology.com/wiki/index.php/Transmission_HowTo]
or
[http://synoblog.superzebulon.org/tag/synology/]
}}}

== tranmissionrpc == 

If you will be using Transmission, then install the transmissionrpc package by running:

{{{
easy_install transmissionrpc
}}}

= Next =

[wiki:InstallWizard/SynologyNAS/FlexGet Install FlexGet]

