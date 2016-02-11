= Windows Service Installer =

This plugin is not very well tested. Somebody please improve this documentation.

Use `flexget service --help` to get the options. Make sure you specify an userame and password when installing the service.


None of the options provided by `flexget service --help` seem to work currently. A workaround is to use 'flexget service install' to install the basic service and then using Windows Services manager to edit the user the service is run under.