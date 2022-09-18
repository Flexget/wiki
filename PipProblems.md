---
title: PipProblems
description: 
published: true
date: 2022-09-18T04:51:06.901Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:04.212Z
---

## Problems with using pip
Make sure your `pip` command uses python 3.6 or newer. 

```cmd
pip --version
```

If this crashes you will need to reinstall pip. Try to remove pip from operating system package manager if possible. You could also run `which pip` and delete the script. Open fresh shell and verify that `python -V` reports 3.6 or newer. Continue with [pip install](https://pip.pypa.io/en/latest/installing.html).

```cmd
pip install --upgrade pip
```

Special note for Arch Linux users. Yours is different.

```cmd
pip2 install --upgrade pip
```

## Pip package issues

```
Traceback (most recent call last):
  File "/usr/lib/python2.7/dist-packages/pip/__init__.py", line 74, in <module>
    from pip.vcs import git, mercurial, subversion, bazaar  # noqa
  File "/usr/lib/python2.7/dist-packages/pip/vcs/mercurial.py", line 9, in <module>
    from pip.download import path_to_url
  File "/usr/lib/python2.7/dist-packages/pip/download.py", line 25, in <module>
    from requests.compat import IncompleteRead
ImportError: cannot import name IncompleteRead
```

Solution in the forum was to remove pip from OS package manager. And the follow [this](https://pip.pypa.io/en/latest/installing/#install-pip).

## Default python version switched
```
[root@foobar ~]# pip install --upgrade flexget
Traceback (most recent call last):
  File "/usr/bin/pip", line 5, in <module>
    from pkg_resources import load_entry_point
  File "/usr/lib/python3.2/site-packages/pkg_resources.py", line 2736, in <module>
    working_set.require(__requires__)
  File "/usr/lib/python3.2/site-packages/pkg_resources.py", line 690, in require
    needed = self.resolve(parse_requirements(requirements))
  File "/usr/lib/python3.2/site-packages/pkg_resources.py", line 588, in resolve
    raise DistributionNotFound(req)
pkg_resources.DistributionNotFound: pip==1.2.1
```

This is most likely because operating system has changed from using python 2.7 to 3.2. Reinstall pip and FlexGet.

## Command not found
If for some reason the flexget executable is not in place even after installing with pip you may get error like.

```cmd
$ flexget -v
-bash: flexget: command not found
```

It might be resolvable by running

```cmd
pip install --upgrade --force-reinstall flexget
```

Setup tools may need to be updated as well, might need to run this command before the previous one.

```cmd
curl https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py | sudo python
```

## Distribute package
```
Traceback (most recent call last):
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/setuptools/command/egg_info.py", line 308, in run
self.add_defaults()
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/setuptools/command/egg_info.py", line 335, in add_defaults
rcfiles = list(walk_revctrl())
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/setuptools/command/sdist.py", line 46, in walk_revctrl
for item in ep.load()(dirname):
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/pkg_resources.py", line 1954, in load
entry = import(self.module_name, globals(),globals(), [name](/name))
ImportError: No module named setuptools_scm.integration

----------------------------------------

Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-jVEBl5/guessit/
```

This is caused by leftover python package distribute. Remove it with command

```cmd
$ sudo pip uninstall distribute
```

## A plugin with the same name is already registered
For some reason the pip leaves files hanging from older version sometimes. If you encounter this it's best to do is update pip and do some cleanup.

Upgrade pip with

```cmd
pip install --upgrade pip
```

We need to know where FlexGet installation is in the filesystem, as this differs per operating system easiest way is to run following command.

```cmd
python -c 'import flexget; print flexget.__file__'
```

Which will print something along

```cmd
/usr/lib/python2.7/site-packages/flexget/
```

Next uninstall FlexGet

```cmd
pip uninstall flexget
```

If you still have the printed directory left, delete it. This should get rid of any extra files hanging around. Next step, reinstall FlexGet.

```cmd
pip install flexget
```

## ImportError: cannot import name IncompleteRead
This is caused by a bug in Ubuntu's pip package. You'll need to uninstall pip with apt, then install with the instructions [here](https://pip.pypa.io/en/latest/installing.html#install-pip).


### Removing leftovers

Removing traces of old FlexGet from your python site-packages, eg.

```cmd
rm /usr/local/lib/python2.6/site-packages/FlexGet-*
```

