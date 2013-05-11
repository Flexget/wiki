OpenWrt is described as a Linux distribution for embedded devices.
[[BR]]
[[BR]]

= Set up environment =

!FlexGet and dependencies currently need ~7MB of free space, plus the stuff you install with opkg (another ~3MB). It can be trimmed down, because there are dependencies only needed for future webui so it would be possible to run FlexGet without them. However easy_install will install them too.

== Python ==

Install python with sqlite3 and yaml. Python-openssl is only necessary for https connections, python-expat for the nzb-plugin.

{{{
opkg install python python-sqlite3 pyyaml
opkg install python-expat
opkg install python-openssl
}}}

{{{
opkg install python-sqlite 
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

If you decide to unpack your packages on an extroot (**recommended**), use the following command:

{{{
pip install flexget -b /your/path/to/extroot/tmp
}}}


This will install !FlexGet and all additional components it requires.

If the installation fails (IOError's, End of file...), it's related to a full filesystem, review your extroot.
 
== Verify installation ==

Run command:

{{{
# flexget -V
FlexGet 1.0r2230
}}}

== Continue ==

[wiki:InstallWizard/Linux/Environment/FlexGet/Scheduling Scheduling]

