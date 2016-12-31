# Installing FlexGet
## Install
```
$ pip3 install flexget
```

`pip3` installs FlexGet to `/opt/bin/flexget`. `/opt/bin` should be in your path if you followed the instructions correctly when you installed `opkg`.

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
