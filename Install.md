= How to install !FlexGet =

== Download ==

First you need to download !FlexGet. You can [http://download.flexget.com download FlexGet distributions from here]. For bleeding edge users, [wiki:Subversion subversion] is available.

= Depencies =

!FlexGet requires some python libraries to work.

== Required ==

[http://pyyaml.org/ PyYAML]

== Recommended ==

For RSS sources:[[BR]]
[http://www.feedparser.org/ feedparser]

For HTML sources and some other modules:[[BR]]
[http://www.crummy.com/software/BeautifulSoup/ BeautifulSoup]

On Debian and Ubuntu you can use apt-get to install all these:

{{{
sudo apt-get install python-yaml python-beautifulsoup python-feedparser
}}}

For other distributions check their package management. If it does not have these packages available you can still install 
them manually by following instructions at library site in question. Or you could use the [http://peak.telecommunity.com/DevCenter/EasyInstall Easy Install] Python installation module. [http://pyyaml.org/ PyYAML], [http://www.crummy.com/software/BeautifulSoup/ BeautifulSoup] and [http://www.feedparser.org/ feedparser] are available.

= Extracting =

Open !FlexGet distribution to any folder you like, suggested path is ~/flexget/ which is used in all examples.

= Running =

Running !FlexGet should be easy, it's designed to be executed from user crontab (daemon mode later perhaps).

Before installing !FlexGet into crontab must [wiki:Configuration write a configuration file] and test that configuration file works.

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
*/30 ~/flexget/flexget.py -q
}}}

Where 30 is the time between executions.

== Manual execution ==

!FlexGet can be tested by executing it manually. See [wiki:Parameters parameters].

To test a configuration file you have written, you can use command:

{{{
python flexget.py -c <config>
}}}

Note that this will download all matches as it would when executed from crontab and skips them on next execution. You can use {{{--test}}} to disable downloading and writing session file which is used to keep application state.

If you want to have additional details about the process, use parameter {{{-d}}}.

= Upgrading =

Safest way to upgrade is to run your old version normally once, then update to new version and if problems arise run application with --reset parameter. This will reset session and learn all current matches as already downloaded items.
