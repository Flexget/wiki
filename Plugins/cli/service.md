= Windows Service Installer =
'''{{{WARNING:}}}''' This plugin is not very well tested. Somebody please improve this documentation.

This CLI command can be used to install a windows service which runs the !FlexGet daemon.

== Usage ==
This plugin requires pywin32 to be installed. Download [https://sourceforge.net/projects/pywin32/files/pywin32/Build%20220/ here].

Use `flexget service --help` to get the options. Make sure you specify an userame and password when installing the service.


None of the options provided by `flexget service --help` seem to work currently. A workaround is to use `flexget service install` to install the basic service and then using Windows Services manager to edit the user the service is run under.