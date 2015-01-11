= Installing !FlexGet on OSX =

''NOTE: Works on 10.6 and 10.7. It also works in 10.5, but after easy_install'ing flexget, you also need to install "simplejson" the same way.''

{{{
sudo easy_install flexget
}}}

Some plugins will require their own installs, e.g.:

{{{
sudo easy_install transmissionrpc
}}}

Some Yosemite (10.10) users have reported issues with easy_install. Using easy_install to install pip, then using pip to install setuptools and flexget has been reported to be successful:

{{{
sudo easy_install pip
sudo pip install setuptools
sudo pip install flexget
}}}

Pip can then be used for upgrades:

{{{
sudo pip install --upgrade setuptools
sudo pip install --upgrade flexget
}}}

When upgrading, it is best practice to unload the Launch Agent to avoid nasty errors, as per below.

== Autorun ==

Create /Users/USERNAME/Library/LaunchAgents/com.flexget.plist with:

{{{
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>  
	<key>Label</key>
	<string>com.flexget</string>
	<key>ProgramArguments</key>
	<array> 
		<string>/usr/local/bin/flexget</string>
		<string>--cron</string>
		<string>execute</string>
	</array>
	<key>Nice</key>
	<integer>1</integer>
	<key>StartInterval</key>
	<integer>900</integer>
	<key>RunAtLoad</key>
	<true/>
</dict>
</plist>
}}}

'''Note''': On some systems, FlexGet installs itself into {{{/bin/flexget}}} instead of {{{/usr/local/bin/flexget}}}; type {{{which flexget}}} to find out where the FlexGet binary is located and modify {{{com.flexget.plist}}} accordingly.

Then:

{{{
launchctl load -w /Users/USERNAME/Library/LaunchAgents/com.flexget.plist
}}}

When upgrading, use this to unload the plist:

{{{
launchctl unload /Users/USERNAME/Library/LaunchAgents/com.flexget.plist
}}}

If you want to check if Flexget is running, use

{{{
launchctl list | grep flexget
}}}

If the process is running, you'll see a process ID in the first column, followed by the last exit status. If the second column isn't 0, check your log file for errors.

Check the launchd man page for other options.

= Other / Deprecated =

== Installing with PIP ==

''Unverified, but this should be the best way''

Install the Python pip module using !MacPorts:

http://www.macports.org/ports.php?by=name&substr=py%25-pip

after that you should be able to install !FlexGet simply with

{{{
py-pip install flexget
}}}


== Other ==

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