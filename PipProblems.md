== Problems with using pip ==

Make sure your `pip` command uses python 2.6-2.7. Some distributions now use python 3.x as a default and !FlexGet does not work with that. 
Python 2.6-2.7 pip may be available under `pip2.7` or other means. If you receive traceback that mentions python3.x you're using wrong pip.

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