= Installing !FlexGet =

=== Download/Install ===

Find the latest version of !FlexGet at http://download.flexget.com/unstable, download and install it by running:

{{{
easy_install http://download.flexget.com/unstable/FlexGet-<insert latest version here>-py2.6.egg
}}}

Note: In future, to update !FlexGet when new versions are released, run the above command with the latest egg.

=== Determine full path to executable ===

Starting from this step, you shouldn't use the root account for anything.

To determine where the !FlexGet command resides run:

{{{
find / -name flexget -type f 2>/dev/null
}}}
{{{
#!comment
Using 'find' because Synology does not support 'where'.
}}}

Example output: `/opt/local/bin/flexget`. It may be different in your environment.
In the following steps, replace /path/to/flexget with the actual path on your system.

=== Verify installation ===

Run command:

{{{
/path/to/flexget -version
}}}

!FlexGet should display it's version number.

=== Configuration ===

Before scheduling !FlexGet you must must [wiki:Configuration write a configuration file] and test that it works correctly. The SQLite database file will get created in the same directory as the configuration file, so make sure the user executing !FlexGet has write access to that path.

!FlexGet is designed to be executed from user crontab (daemon mode coming later).

== Next ==

[wiki:InstallWizard/SynologyNAS/FlexGet/Scheduling Scheduling]
