= As a Python package =
This is the recommended method as it mirrors how you would install !FlexGet on just about any other system. You will need to be logged into the Synology NAS as root to install packages.

== ipkg ==

The first step is to install `ipkg`, a package manager for Synology (and other systems). Follow the instructions at:

[http://forum.synology.com/wiki/index.php/Overview_on_modifying_the_Synology_Server,_bootstrap,_ipkg_etc]

== System dependencies ==

You'll need to install Python 2.7, setuptools, and sqlite. setuptools includes `easy_install`, which we will use to install `pip`. sqlite is required by !FlexGet.

{{{
$ ipkg install python27
$ ipkg install py27-setuptools
$ ipkg install sqlite
}}}

== Transmission ==

It is highly recommended that you use the Transmission !BitTorrent client instead of the built-in client. Transmission can also be installed via `ipkg`.

{{{
$ ipkg install transmission
}}}

== pip ==

Use `easy_install` to install `pip`, which is a much more user-friendly Python package manager. `easy_install` installs `pip` into `/opt/local/bin`, so add that to your `PATH` variable if it is not already present. Once installed, update use `pip` to update itself the latest version.

{{{
$ easy_install-2.7 pip
$ pip install --upgrade pip
}}}

If using Transmission, you will need to install the `transmissionrpc` package.

{{{
$ pip install transmissionrpc
}}}

== Next ==

You're ready to [wiki:InstallWizard/SynologyNAS/FlexGet install FlexGet].

= Using the synocommunity package =
The synocommunity repository [https://synocommunity.com/] includes a !FlexGet package. If you are less comfortable with the command line, you will probably find this method easier. It may, however, be more difficult to maintain. You must also wait for the package maintainers to update the !FlexGet package; with the above method, updates to !FlexGet may be installed as soon as they are released.

Follow the homepage instructions to add synocommunity to your NAS, and then install Python and !FlexGet through the web interface. The config file will be available at `/usr/local/flexget/var/config.yml`.
