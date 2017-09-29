# [Install Wizard](/InstallWizard) > [SynologyNAS](/InstallWizard/SynologyNAS) > PythonPackage

## Caveats

<div class="alert alert-warning" role="alert">
  FlexGet supports Python 2.7, 3.3, 3.4 and 3.5. Python 3.6 is not yet supported.
</div>

This method uses the Python installation available in DSM's Package Center. As such, it will only work while the version of Python available there is one of those listed above. At time of writing, the DSM package provides Python 3.5.1.

## Install Python

Go to the DSM Package Center and install the Python 3 package.

## Install FlexGet

Before proceeding any further, you'll want to make sure that whatever location `pip` installs to is in your `PATH` so that you can access `flexget` easily.

Install using the following command:

```
pip3 install flexget
```

## Verify installation
Run the following command, and FlexGet will display its version number:

```
$ flexget --version
2.3.42
You are on the latest release.
```

## Configuration
Before you can run FlexGet you must must [write a configuration file](/Configuration) and test that it works correctly. FlexGet stores a number of files in the same directory as its config file so make sure the user that will be executing FlexGet can write to the appropriate path.

## Next
Set up FlexGet to run as a [system service](/InstallWizard/SynologyNAS/Upstart).