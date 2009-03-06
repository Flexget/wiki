= How to install !FlexGet =

== Download ==

First you need to download !FlexGet. You can download !FlexGet distributions from [http://download.flexget.com here]. For bleeding edge users, [wiki:Subversion subversion] is available.

= Depencies =

!FlexGet requires few python libraries to work, strictly speaking only PyYAML is needed but other are required by most modules.

== Required ==

[http://pyyaml.org/ PyYAML]

== Recommended ==

[http://www.feedparser.org/ feedparser] - required for RSS sources[[BR]]

== Debian, Ubuntu and similar ==

On Debian and Ubuntu you can use apt-get to install all these:

{{{
sudo apt-get install python-yaml python-feedparser
}}}

For other distributions check their package management. If it does not have these packages available you can still install 
them manually by following instructions at library site in question. Or you could use the [http://peak.telecommunity.com/DevCenter/EasyInstall Easy Install] Python installation module. [http://pyyaml.org/ PyYAML] and [http://www.feedparser.org/ feedparser] are available.

== OS X ==

On Mac OS X, you can use [http://www.macports.org/install.php MacPorts] to install PyYAML:

{{{
sudo port install py25-yaml
}}}


== Windows ==

Installing libraries on windows may be a bit more troublesome, your best shot is to install [http://peak.telecommunity.com/DevCenter/EasyInstall Easy Install] and install require libraries by using it.[[BR]]''Note: Please add more / improve instructions if you install !FlexGet on windows.''

= Install =

Just extract !FlexGet archive to any folder you like, suggested path is ~/flexget/ which is used in all examples. On Windows "C:\Program Files\FlexGet\" is obvious choice.

= Setup =

[wiki:Configuration Configure] and test !FlexGet before setting up scheduled executions.

'''Manual execution'''

!FlexGet can be tested by executing it manually. See [wiki:Parameters parameters].

To test a configuration file you have written, you can use command:

{{{
python flexget.py -c <config>
}}}

Note that this will download all matches as it would when executed from crontab and skips them on next execution. You can use {{{--test}}} to disable downloading and writing session file which is used to keep application state.

If you want to have additional details about the process, use parameter {{{-d}}}.

= Scheduling =

Before scheduling !FlexGet you must must [wiki:Configuration write a configuration file] and test that it works correctly.

== Windows ==

There are few tricks with scheduling !FlexGet under Windows. At first glance "Scheduled Tasks" does not seem to allow execution intervals more frequently than once per day. There is however way to do it, and it is explained very well in [http://lonewolf-online.net/computers/kb/windows/guide-windows-task-scheduler/ here].[[BR]]''Note: Please add more / improve instructions if you install !FlexGet on windows.''

== Linux, using cron ==

Running !FlexGet should be easy, it's designed to be executed from user crontab (daemon mode later perhaps).

To change default editor for crontab, you can use command:

{{{
export EDITOR=nano
}}}

^You may wish to add this into your ~/.bashrc so it will be always the default editor^

To edit user crontab execute command:

{{{
crontab -e
}}}

Enter one new line on crontab:

{{{
@hourly ~/flexget/flexget.py -q
}}}

This will run !FlexGet every hour. You may run it more frequently as well, but I wouldn't recommend going below 30 minutes since it will cause unnecessary load on RSS-feeds and pages you're subscribed to. Some feed providers even ban your IP if you request feed too often.

To run more often you may use crontab in form of:

{{{
*/30 * * * * ~/flexget/flexget.py -q
}}}

Where 30 is the time between executions.

=== GUI way ===

Instead of editing by hand, you could try one of these.

[http://www.arquired.es/users/aldelgado/proy/gcrontab/ gcrontab] - GTK bases crontab editor
[[BR]]
[http://www.kde.org/ kcron] - the KDE crontab editor

== OS X (Tiger, Leopard) using launchd ==

[http://en.wikipedia.org/wiki/Launchd Launchd] is what you should be using on OS X.

Create a new file named '''~/Library/LaunchAgents/com.flexget.plist''' and paste the following text into it:

{{{
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple Computer//DTD PLIST 1.0//EN"
"http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>  
        <key>Label</key>
        <string>com.flexget</string>
        <key>ProgramArguments</key>
        <array> 
                <string>/usr/local/lib/flexget/flexget.py</string>
                <string>-q</string>
        </array>
        <key>LowPriorityIO</key>
        <true/>
        <key>Nice</key>
        <integer>1</integer>
        <key>StartCalendarInterval</key>
        <dict>  
                <key>Minute</key>
                <integer>50</integer>
        </dict>
</dict>
</plist>
}}}

Now, log out and back in, or run the following:

{{{
sudo launchctl load ~/Library/LaunchAgents/com.flexget.plist
}}}

It will now run each hour at the 50 minute mark. (14.50, 15.50, ...)

= Upgrading =

Safest way to upgrade is to run your old version normally once, then update to new version and if problems arise run application with --reset parameter. This will reset session and learn all current matches as already downloaded items.