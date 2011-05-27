OpenWrt is described as a Linux distribution for embedded devices.
[[BR]]
[[BR]]

= Set up environment =

Python, !FlexGet and dependencies currently need ~7MB of free space. It can be trimmed down, because there are dependencies only needed for future webui so it would be possible to run FlexGet without them. However easy_install will install them too.

== Python ==

Install python with sqlite3 and yaml. Python-openssl is only necessary for https connections, python-expat for the nzb-plugin.

{{{
opkg install python python-sqlite3 pyyaml
opkg install python-expat
opkg install python-openssl
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

