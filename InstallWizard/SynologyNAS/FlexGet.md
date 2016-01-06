= Installing !FlexGet =

== Install ==

{{{
$ pip install flexget
}}}

`pip` installs !FlexGet to `/opt/local/bin/flexget`. If `/opt/local/bin` isn't in your `PATH`, you should add it.

== Verify installation ==

Run the following command, and !FlexGet should display it's version number:

{{{
$ flexget --version
1.2.422
You are on the latest release.
}}}

== Configuration ==

Before scheduling !FlexGet you must must [wiki:Configuration write a configuration file] and test that it works correctly. The SQLite database file will get created in the same directory as the configuration file, so make sure the user executing !FlexGet has write access to that path.

== Next ==

Set up !FlexGet to run as a [wiki:InstallWizard/SynologyNAS/Upstart system service].
