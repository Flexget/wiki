OpenWrt is described as a Linux distribution for embedded devices.
[[BR]]
[[BR]]

= Set up environment =

Python, !FlexGet and dependencies need ~7MB^1^ of free space. python-openssl is only necessary for https connections, python-expat for the nzb-plugin.

^1. FlexGet has now few dependencies that are fairly large (~10MB) .. These are only needed for future webui so it would be possible to run FlexGet without them. However easy_install will install them too.^

== Python ==

{{{
opkg install python
opkg install python-sqlite3
opkg install python-expat
opkg install python-openssl
opkg install pyyaml
}}}

== easy_install ==

{{{
opkg install distribute
}}}

== Install ==

Run command:

{{{
easy_install flexget
}}}

This will install !FlexGet and all additional components it requires.

== Verify installation ==

Run command:

{{{
# flexget -V
FlexGet 1.0r2230
}}}

== Continue ==

[wiki:InstallWizard/Linux/Environment/FlexGet/Scheduling Scheduling]

