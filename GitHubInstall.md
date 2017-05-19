# GitHub Install
## Notes

 * Requires Python 2.7 or 3.3-3.5, virtualenv, and git client
 * This where we develop

## Initial clone
To checkout use this command:

```bash
$ git clone https://github.com/Flexget/Flexget.git ~/flexget-dev
```

You can use whatever directory you like in place of `~/flexget-dev`.

After checkout is complete, you need to initialize the environment.

Make sure the `python` command uses Python 2.7 or 3.3-3.6. On some systems with multiple python installations, you may need to use a command specific to a particular version, such as `python2.7` or `python3`.

```bash
$ python -V
```

## `virtualenv`
Initialize a `virtualenv` in your checkout directory:

```bash
$ virtualenv ~/flexget-dev
```
**NOTE:** If you need to use the Python packages already installed, such as the `deluge` package for use with the [`deluge`](/Plugins/deluge) plugin, create your virtualenv with the `--system-site-packages` flag.


Once the virtualenv has been created, we need to install the checked-out copy of FlexGet inside it.

Make sure you are using the pip installed in your virtualenv by either activating the `virtualenv` first, or explicitly calling `bin/pip` as shown below. (On Windows, use `Scripts/` any place you see `bin/` in this guide.)

The `-e` flag to pip says this should be an editable install, meaning it uses the files directly in the checkout rather than installing a package in site-packages.

```bash
$ cd ~/flexget-dev
$ bin/pip install -e .
```

Once this is completed you'll have FlexGet installed in a virtualenv.

You can execute FlexGet via:

```bash
$ ~/flexget-dev/bin/flexget execute
```

## Upgrading
To upgrade your install, first pull the changes from our repo:

```bash
$ cd ~/flexget-dev
$ git pull
```

If the dependencies have changed, you can reinstall to upgrade all the dependencies:

```bash
$ bin/pip install --upgrade -e .
```

## Become a contributor
If you're interested in helping to improve FlexGet, or adding new plugins, please read our [contribute page](/Contribute).
