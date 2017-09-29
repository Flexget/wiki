# [Install Wizard](/InstallWizard) > SynologyNAS

There are a few different ways to go about running FlexGet on your NAS. They are listed below in order of preference.

## [Docker container](/InstallWizard/SynologyNAS/Docker)

Running FlexGet in a Docker container gives you the ultimate level of control over its environment.

## [Local Python package](/InstallWizard/SynologyNAS/PythonPackage)

<div class="alert alert-warning" role="alert">
  FlexGet supports Python 2.7, 3.3, 3.4 and 3.5. Python 3.6 is not yet supported.
</div>

This method uses the Python installation available in DSM's Package Center. As such, it will only work while the version of Python available there is one of those listed above. At time of writing, the DSM package provides Python 3.5.1.

## synocommunity package

The [synocommunity](/https://synocommunity.com/) repository includes a FlexGet package for DSM.

If you are less comfortable with the command line, you will probably find this method easier. It may, however, be more difficult to maintain. You must also wait for the package maintainers to update the FlexGet package; with the above method, updates to FlexGet may be installed as soon as they are released.

Follow the homepage instructions to add synocommunity to your NAS, and then install Python and FlexGet through the web interface. The config file is located at `/usr/local/flexget/var/config.yml`.
