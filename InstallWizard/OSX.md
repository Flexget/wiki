= Installing !FlexGet on OSX =

''TODO: Someone needs to write this neatly ...''

== Installing with PIP ==

''Unverified, but this should be the best way''

http://py-pip.darwinports.com/

after that you should be able to install !FlexGet simply with

{{{
py-pip install flexget
}}}

= Other / Deprecated =

 * OSX 10.5 uses python 2.5
 * OSX 10.6 uses python 2.6

Easy install tools needs to be compiled.
You can then use the InstallEggMac guide to get the dependencies, and install the egg.

 * [wiki:InstallOSX see old 0.9.x guide]
 * [wiki:InstallEggMac Notes for 1.0 in mac 10.6]

'''Gathered from irc'''

{{{
> aha!
> got it!
> :-)
> flexget with mac ports
> export PYTHONPATH=/opt/local/Library/Frameworks/Python.framework/Versions/2.6/lib/python2.6/site-packages
> woot
}}}

== Installing through Fink ==

[http://www.finkproject.org/ Fink] has !FlexGet in unstable, as of 2010-07-24.  You should just need to run 'fink install flexget' with unstable enabled and it will install all dependencies.

The version in fink seems to be quite old.
