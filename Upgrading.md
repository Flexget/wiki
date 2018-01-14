# Upgrading
## Check current version

Start by checking what version you currently have with command:

```
flexget -V
```

***Git Users:*** You can check the latest release you have by getting new tags with `git fetch --tags` then running `git describe`

Write this down somewhere.

### Backup database(s) (optional)
In case you wish to roll back to previous version you will need to make backup of your database since running new version will upgrade it and downgrade is not supported.

Each configuration file has corresponding database file, so for example config.yml will have db-config.sqlite

Copy this file to backup file containing the version number you are were last using, e.g. db-config.sqlite_1.1.59

## Upgrade with PIP

If you have followed normal installation procedure follow this.
If you are using cron and have short cron interval, comment FlexGet out from the cron. If you are running the daemon, you should [stop the daemon](/Daemon) until the upgrade is complete and you verify your config file works with the updated version.

There has been alot of errors arising from setuptools package being out of date and failing an upgrade.
Please make sure to upgrade setuptools.

```cmd
pip install --upgrade setuptools
pip install --upgrade flexget
```

[Problems with pip](/PipProblems)

Git users can just run `git pull`. If the dependencies have changed, you'll also have to run `bin/pip install -e .` again to upgrade them.

## Upgrade GIT checkout

If you are running GIT checkout (development environment). You may need to run following commands at the checkout directory after pulling code:

```cmd
bin/pip install --upgrade -r requirements.txt
bin/python setup.py develop
```

## Verify
Check if your configuration file is still valid, there may have been some changes to it.

```cmd
flexget check
```

If your configuration doesn't pass check, ave a look at [upgrade actions](/UpgradeActions) to see if there are any actions you must take. The behavior of certain plugins may also have changed, so check [upgrade actions](/UpgradeActions) even if your config is passing.

For example, if you were running 1.1.2 follow all the steps above this revision.

### Problems ?
If you encounter problems, there are ways to get [help](/NeedHelp) !

If you receive errors about database upgrades please report them via a [ticket](https://github.com/Flexget/Flexget/issues). If you do not care about the history for that plugin, you can reset the database for that plugin with `--reset-plugin PLUGINNAME` to get it working again.
