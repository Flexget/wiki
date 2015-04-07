= Sleep =

Sleep during the specified task execution phase.

(Specifically for setting limits on how often a particular domain is accessed, you can use [wiki:Plugins/domain_delay domain_delay].)

== Phase Order ==
Task execution in Flexget takes the form of a series of phases, which run in this order by default:

{{{
start
input
metainfo
filter
download
modify
output
learn
exit
}}}
There is also an `abort` phase which is triggered if an error occurs during some other phase. This can occur at any time, depending upon when the error happens, so is not part of the specified order list above. However, you can use it as your specified phase for this plugin.

Which phase plugins operate in can be seen by running the following command from the command line:
{{{
flexget plugins
}}}
This list also shows the priority a plugin has set by default in each phase. (See below for more about using priority in combination with this plugin.)

== Configuration ==
Configuration can take one of two forms. In the first, simpler form, sleep is always executed during the `start` phase, and delays execution for the specified number of seconds.
{{{
sleep: <seconds>
}}}

The second form is more versatile and is available as of v1.2.298. It allows you to delay execution during a specified phase (from the list above) in addition to specifying the number of seconds.
{{{
sleep:
  seconds: <seconds>
  phase: <phase>
}}}

== Using Sleep in Combination with Plugin Priorities ==
Priority determines which order plugins execute in. As an example, the [wiki:Plugins/set set] plugin has a priority number of 128 during the metainfo phase. Most if not all other plugins running during this phase have a lower number for priority, which means they run later. You can change the priority of plugins using [wiki:Plugins/plugin_priority plugin_priority], which may be needed in combination with this task.

By default, the sleep plugin has a priority of 255 in all phases, meaning it will run at the beginning of the phase during which it is set to run. However, you may need to delay execution of a phase between two plugins that run during that phase.

For example, imagine a scenario with two output plugins - one that modifies the stored location of files in a torrent program, and the other which passes the location of files to another program. If these steps execute without enough delay between them, the second program may receive paths that do not yet exist as the torrent program has not had time to finish moving files around.

A sample configuration for the above scenario is listed below, and uses [wiki:Plugins/deluge deluge] and [wiki:Plugins/aria2 aria2], which are both output plugins. Deluge is a torrent client, and aria2 is a download manager. This example gets a list of torrents from Deluge, changes their file locations, and then passes the new locations to aria2. The sleep plugin is used to ensure enough time has passed between issuing the move command in Deluge and giving the new paths to aria2. The default priorities for deluge is 135, for aria2 is 128, and for sleep is 255. Therefore, the priority of sleep is changed to 129, so it will run between them.
{{{
from_deluge:
  filter: seeding
deluge:
  path: /my/new/path
aria2:
  do: add-new
  uri: 'http://ftp.example.com:21/my/new/path/{{title}}'
sleep:
  phase: output
  seconds: 10
plugin_priority:
  sleep: 129
}}}