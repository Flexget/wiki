= Configuration =

In order to use !FlexGet you'll need to create a configuration file. 

!FlexGet uses [http://en.wikipedia.org/wiki/Yaml Yaml] markup in configuration file. 

{{{
#!html
<h2 style="color: red">Common mistakes, read at least these!</h2>
}}}

 * Indentation level. Always use (multiples of) '''2 spaces''' and '''never''' use tab-key!
 * Plugins are supposed to be indented at the same level (rss, series, download etc). Some plugins may allow other plugins inside of them.
 * Missing colons. Pay special attention to these when looking at the examples and documentation
 * If text value contains any of `{}[]%:` characters it must be quoted with `''`
 * If you want to pass a number as a text (ie. series ''24''), value must be quoted with `''`

=== Location ===

By default !FlexGet tries to find `config.yml` from current path and in `~/.flexget/` (`C:\Users\YOURUSER\flexget\` on Windows 7, and `C:\Documents and Settings\YOURUSER\flexget\` on XP). Creating the `~/.flexget/` directory and placing your `config.yml` in there is considered currently as the best practice.

== Step by Step Configuration Tutorial ==
The configuration is a hierarchy constructed of various components. The main component of any config are the tasks, so we will start there.
{{{
tasks:
}}}
The line ends in a colon, which means we will be defining this section on the lines following. We then indent (2 spaces) everything that belongs to this section. The tasks sections is made up of all your individual tasks, which can be named whatever we want. Let's make one called `test task`.
{{{
tasks:
  test task:
}}}
This line defining the task name (test task) also ends with a colon, which means we will be defining what belongs in this task on the following lines with another indent (2 more spaces.) The contents of an individual task are always [wiki:Plugins plugins]. There are three main types of plugins we normally want in a task, an [wiki:Plugins#inputs input] (where do you want !FlexGet to look for things?), a [wiki:Plugins#filter filter] (which of those things do you want?) and an [wiki:Plugins#output output] (what do you want !FlexGet to do with those things?). Let's start by adding an input plugin to our task, `test task`. In this case we will use the [wiki:Plugins/rss rss] plugin as our input. The indentation of rss is increased and means that it belongs under the test task.
{{{
tasks:
  test task:
    rss:
}}}
We aren't finished yet, this line ends with a colon, which means we need to provide the next section, which would be the options for the rss plugin. When configuring any plugin, visit that plugin's [wiki:Plugins wiki page] to find out what format the options for that plugin should be in. The most simple configuration format for the rss plugin allows us to just define the url for the rss feed. If the plugin has more complicated configuration, follow the indentation shown in the plugin documentation. Note that if you simply copy & paste examples from documentation you must increase the indentation to correct level.

{{{
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
}}}

Our input plugin will create an entry for every item that comes into the rss feed, but we still need to tell !FlexGet which of those items we want. We do this with a [wiki:Plugins#filter filter] plugin. One of the most common is the [wiki:Plugins/series series] plugin, so we will configure that here. This plugin will belong to our `test task` so we remain at the same indentation level, 2 more spaces than `test task`.
{{{
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
}}}
Now we must consult the [wiki:Plugins/series series] wiki page to determine how to configure the series plugin. There are two formats the series plugin configuration can take, we will stick with the simple one in this tutorial. (eventually you may want to switch to the [wiki:Plugins/series/per_group_settings grouped format]) In the simple format, the series plugin just takes a list of the series you want. Since our last line ended with a colon, we go to the next line with 2 more spaces. Each item in our list will be at this same indentation level, and start with '- ' so:
{{{
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
}}}
The series plugin also allows defining options per show, which we will do with our next show.
{{{
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
}}}
Since we are defining options for this show, we ended the line with a colon. This normally means we define the options on the next line with 2 more spaces. There is a slight exception when defining options for a list item, in that we have to go 2 more spaces than the actual word, for a total of 4 spaces. Here we will define the `quality` option of the series plugin to only allow 720p copies of this show to be downloaded.
{{{
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
          quality: 720p
}}}
Now that we have an input and a filter plugin, we need to tell !FlexGet what we want to do with the entries that are accepted by our filter. We do this with an [wiki:Plugins#output output plugin]. One common output plugin is the [wiki:Plugins/download download] plugin, which we could use to save our items to a watch directory from a bittorrent or nzb client. (if you are using [wiki:Plugins/deluge deluge] or [wiki:Plugins/transmission transmission] you may want to consider using its dedicated output plugin instead)
{{{
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
          quality: 720p
    download:
}}}
The [wiki:Plugins/download download] plugin also has a very simple configuration option, in which we can just define the path where we would like it to save our content.
{{{
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
          quality: 720p
    download: /home/me/watchdir/
}}}
Congratulations, we now have a fully functioning config file. You can continue to add more tasks to your config file to complete different jobs, or customize this one further. Remember to consult the [wiki:Plugins plugins] wiki page to choose your plugins, and read the individual page for each plugin to figure out how to configure that specific plugin.

'''Now just sit back, and let !FlexGet do the work for you! '''
== Common misconceptions ==

 * Plugin order doesn't matter, you can list them in any order you like. Most logical order would be `inputs` -> `filters` -> `outputs`.
 * Task order doesn't matter, tasks are executed in seemingly random order. Use [wiki:Plugins/priority priority] plugin priorize tasks when necessary.
 * You cannot list plugins, ie. [wiki:Plugins/rss rss] twice in a single task. This is limited by the chosen simpler syntax in the configuration file. Instead see [wiki:Plugins/preset preset] plugin.

== Tips ==

=== Test execution ===

Executes all tasks, but doesn't write anything into disk.

{{{
flexget --test execute
}}}

=== Display more process details ===

Adding `-v` parameter will display useful information about task(s) content.

=== Check configuration syntax ===

When you create or modify configuration try running !FlexGet with `check` parameter. It will go through the configuration file and report any irregularities found. If you used recommended configuration name and location, simply executing `flexget check` will do this. If this doesn't report any problems you should have fully working configuration file.

== References ==

 * See [wiki:Cookbook/Series/Preset how to manage series] for how to refine this example into real world usage (with multiple tasks).
 * Continue into [wiki:Plugins plugins] to learn all about available plugins you may use in you configuration file.
 * [wiki:StillConfusedYaml Still confused about Yaml syntax?]