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

== Linux, OSX and similar ==

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

= Upgrading =

Safest way to upgrade is to run your old version normally once, then update to new version and if problems arise run application with --reset parameter. This will reset session and learn all current matches as already downloaded items.