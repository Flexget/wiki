== Problems with using pip ==

Make sure your `pip` command uses python 2.6-2.7. Some distributions now use python 3.x as a default and !FlexGet does not work with that. 
Python 2.6-2.7 pip may be available under `pip2.7` or other means. If you receive traceback that mentions python3.x you're using wrong pip.
To verify which version pip is using you can use:

{{{
pip --version
}}}

If this crashes you will need to reinstall pip. Try to remove pip from operating system package manager if possible. You could also run "which pip" and delete the script. Open fresh shell and verify that `python -V` reports 2.6-2.7. Continue with [https://pip.pypa.io/en/latest/installing.html pip install].


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

This is most likely because operating system has changed from using python 2.7 to 3.2. Pip was installed on 2.7 but now that the script is ran it uses default python which is 3.2. You will need to re-install pip for python 2.7. This can happen for any python executable, including !FlexGet if the operating system changes default python version. Re-installing the packages with correct python version will resolve the issue.

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