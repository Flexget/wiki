OpenWrt is described as a Linux distribution for embedded devices.
[[BR]]
[[BR]]

= Set up environment =

!FlexGet and dependencies currently need ~7MB of free space, plus the stuff you install with opkg (another ~3MB). It can be trimmed down, because there are dependencies only needed for future webui so it would be possible to run FlexGet without them. However easy_install will install them too.

== Python ==

Install python with sqlite3 and yaml. Python-openssl is only necessary for https connections, python-expat for the nzb-plugin.

{{{
opkg install python python-sqlite3 pyyaml
opkg install python-sqlite
opkg install python-expat
opkg install python-openssl

opkg install python-bzip2
}}}


== easy_install ==

{{{
opkg install distribute
}}}

== pip ==
[http://www.pip-installer.org/en/latest/usage.html pip usage:]

{{{
easy_install pip
}}}


== Install ==

Run command:

{{{
pip install flexget
}}}

If you decide to unpack your packages on an external storage (**recommended**), use the following command: (this is needed if you get a 'No space left on device' error)

{{{
pip install flexget -b /your/path/to/extstorage/tmp
}}}


This will install !FlexGet and all additional components it requires.

If the installation fails (IOError's, End of file...), it's related to a full filesystem, review your extroot.
 
== Verify installation ==

Run command:

{{{
# flexget -V
FlexGet 1.0r2230
}}}


== Alternate Install method for Flexget ==

In some cases, using pip to extract the tar on an external path might still not be enough to have enough space on the / partition of the router to be able to install flexget.

You can use the following to set Python's path to point to the external storage so that it installs all packages on your external path e.g an attached USB flash drive
Once you have completed the above step "opkg install distribute"

Run command:

export PYTHONPATH=$PYTHONPATH:/mnt/sda1      [Where /mnt/sda1/ is my mounted USB flash drive]
easy_install -d /mnt/sda1/ flexget           [Install "Flexget" using easy_install]

You can also put the above export command in the "startup" section of openWRT so that path is loaded at router bootup.





== Continue ==

[wiki:InstallWizard/Linux/Environment/FlexGet/Scheduling Scheduling]
