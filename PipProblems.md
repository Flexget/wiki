== Problems with using pip ==

Make sure your `pip` command uses python 2.7, 3.4 or newer. 

{{{
pip --version
}}}

If this crashes you will need to reinstall pip. Try to remove pip from operating system package manager if possible. You could also run `which pip` and delete the script. Open fresh shell and verify that `python -V` reports 2.7, 3.4 or newer. Continue with [https://pip.pypa.io/en/latest/installing.html pip install].


== Default python version switched ==

{{{
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
}}}

This is most likely because operating system has changed from using python 2.7 to 3.2. Reinstall pip and !FlexGet.

== Command not found ==

If for some reason the flexget executable is not in place even after installing with pip you may get error like.

{{{
$ flexget -v
-bash: flexget: command not found
}}}

It might be resolvable by running

{{{
pip install --upgrade --force-reinstall flexget
}}}

Setup tools may need to be updated as well, might need to run this command before the previous one.

{{{
curl https://bitbucket.org/pypa/setuptools/raw/bootstrap/ez_setup.py | sudo python
}}}

== Distribute package ==

{{{
Traceback (most recent call last):
File "", line 1, in
File "/tmp/pip-build-jVEBl5/guessit/setup.py", line 78, in
setup(**args)
File "/usr/local/lib/python2.7/distutils/core.py", line 151, in setup
dist.run_commands()
File "/usr/local/lib/python2.7/distutils/dist.py", line 953, in run_commands
self.run_command(cmd)
File "/usr/local/lib/python2.7/distutils/dist.py", line 972, in run_command
cmd_obj.run()
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/setuptools/command/egg_info.py", line 179, in run
self.find_sources()
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/setuptools/command/egg_info.py", line 254, in find_sources
mm.run()
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/setuptools/command/egg_info.py", line 308, in run
self.add_defaults()
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/setuptools/command/egg_info.py", line 335, in add_defaults
rcfiles = list(walk_revctrl())
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/setuptools/command/sdist.py", line 46, in walk_revctrl
for item in ep.load()(dirname):
File "/usr/local/lib/python2.7/site-packages/distribute-0.6.14-py2.7.egg/pkg_resources.py", line 1954, in load
entry = import(self.module_name, globals(),globals(), ['name'])
ImportError: No module named setuptools_scm.integration

----------------------------------------

Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-jVEBl5/guessit/
}}}

This is caused by leftover python package distribute. Remove it with command

{{{
$ sudo pip uninstall distribute
}}}

== A plugin with the same name is already registered ==

For some reason the pip leaves files hanging from older version sometimes. If you encounter this it's best to do is update pip and do some cleanup.

Upgrade pip with

{{{
pip install --upgrade pip
}}}

We need to know where !FlexGet installation is in the filesystem, as this differs per operating system easiest way is to run following command.

{{{
python -c 'import flexget; print flexget.__file__'
}}}

Which will print something along

{{{
/usr/lib/python2.7/site-packages/flexget/
}}}

Next uninstall !FlexGet

{{{
pip uninstall flexget
}}}

If you still have the printed directory left, delete it. This should get rid of any extra files hanging around. Next step, reinstall !FlexGet.

{{{
pip install flexget
}}}

== !ImportError: cannot import name !IncompleteRead ==

This is caused by a bug in Ubuntu's pip package. You'll need to uninstall pip with apt, then install with the instructions [https://pip.pypa.io/en/latest/installing.html#install-pip here].