# Configuration

On this page:
- [Introduction](#introduction)
- [Location](#location)
- [Top-Level Keys](#top-level-keys)
- [Step-by-Step Configuration Tutorial](#step-by-step-configuration-tutorial)
- [Common Misconceptions](#common-misconceptions)
- [Tips](#tips)
- [References](#references)

## Introduction
In order to use FlexGet you'll need to create a configuration file. 

FlexGet uses [YAML](http://en.wikipedia.org/wiki/Yaml) markup in the configuration file. YAML is a way of defining sets of keys (such as plugin names or options) and values (such as series names or path to download files).


<div class="alert alert-warning" role="alert">
Following are some common mistakes; read at least these notes!
</div>

 * Indentation level: always use (multiples of) **two spaces** and **never** use the `tab` key!
 * Plugin indentation: Plugin names are supposed to be indented at the same level (`rss`, `series`, `download`, etc). (Some plugins may allow other plugins inside of them, in which case the sub-plugins should be indented by additional spaces.)
 * Missing colons: Pay special attention to these when looking at the examples and documentation.
 * If a text value contains any of these characters `{}[]%:` it must be quoted with `''` (apostrophes).
 * If you want to pass a number as a text (i.e. the series *24*), the value must be quoted with `''` (apostrophes).
 * See [pitfalls](/PitFalls) for more common errors and mistakes.

## Location
By default FlexGet tries to find `config.yml` from several places, in this order:
- The current path
- The `virtualenv` path (only if you are running FlexGet installed in a `virtualenv`)
- `~/.flexget/` (`C:\Users\YOURUSER\flexget\` on Windows 7, and `C:\Documents and Settings\YOURUSER\flexget\` on Windows XP)
- `~/.config/flexget` (only on Linux)

The first path containing a config file will be used. Creating the `~/.flexget/` directory and placing your `config.yml` in there is currently considered a best practice. You can also use the `-c` [CLI](/CLI) argument to manually specify a config file name (and path) when FlexGet is run.

## Top-Level Keys
In YAML, indendation is crucially important. Most of your time will be spent with keys  that are indented at least two spaces. Following are the top-level keys. In other words, these are never indented.

- `tasks`
- `templates`
- `schedule`
- `web_server`
- `irc`

Everything else in FlexGet is indented under one of the above keys. For example, your tasks are placed under `tasks`, and plugins are placed within those tasks.

## Step-by-Step Configuration Tutorial
The configuration is a hierarchy constructed of various components. The main component of any config are the tasks, so we will start there.
```yaml
tasks:
```
The line ends in a colon, which means we will be defining this section on the lines following. We then indent (with two spaces) everything that belongs to this section. The tasks sections is made up of all your individual tasks, which can be named whatever we want. Let's make one called `test task`.
```yaml
tasks:
  test task:
```
This line defining the task name (`test task`) also ends with a colon, which means we will be defining what belongs in this task on the following lines with another indent (two more spaces.)

The contents of an individual task are always [plugins](/Plugins). There are three main types of plugins we normally want in a task, an [input](/Plugins#inputs) (where do you want FlexGet to look for things?), a [filter](/Plugins#filter) (which of those things do you want?), and an [output](/Plugins#output) (what do you want FlexGet to do with those things?).

Let's start by adding an input plugin to our task, `test task`. In this case we will use the [rss](/Plugins/rss) plugin as our input. The indentation of rss is increased and means that it belongs to the `test task`.
```yaml
tasks:
  test task:
    rss:
```
We aren't finished yet; this line ends with a colon, which means we need to provide the next section, which would be the options for the rss plugin.

When configuring any plugin, visit that plugin's [wiki page](/Plugins) to find out what format the options for that plugin should be in. The most simple configuration format for the rss plugin allows us to just define the url for the rss feed. If the plugin has more complicated configuration, follow the indentation shown in the plugin documentation.

**NOTE**: If you copy and paste examples from the documentation, you must increase the indentation so it is within your task.

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
```

Our input plugin will create an entry for every item that comes into the RSS feed, but we still need to tell FlexGet which of those items we want.

We do this with a [filter](/Plugins#filter) plugin. One of the most common is the [`series`](/Plugins/series) plugin, so we will configure that here. This plugin will belong to our `test task` so we remain at the same indentation level, two more spaces than `test task`.

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
```

Now we must consult the [`series`](/Plugins/series) wiki page to determine how to configure the series plugin. There are two formats the series plugin configuration can take; we will stick with the simple one in this tutorial. (Eventually, you may want to switch to the [grouped format](/Plugins/series/per_group_settings).)

In the simple format, the series plugin just takes a list of the series you want. Since our last line ended with a colon, we go to the next line with two more spaces. Each item in our list will be at this same indentation level, and start with `- ` (dash followed by a space), as such:

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
```
The series plugin also allows defining options per show, which we will do with our next show.

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
```
Since we are defining options for this show, we ended the line with a colon. This normally means we define the options on the next line with two more spaces.

There is a slight exception when defining options for a list item, in that we have to go two spaces from the start of the word on the previous line, for a total of four spaces. Here we will define the [`quality`](/Plugins/series/quality) option of the series plugin to only allow 720p copies of this show to be downloaded.

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
          quality: 720p
```
Now that we have an input and a filter plugin, we need to tell FlexGet what we want to do with the entries that are accepted by our filter. We do this with an [output plugin](/Plugins#output).

One common output plugin is the [`download`](/Plugins/download) plugin, which we could use to save our items to a watch directory for a bittorrent or nzb client. (If you are using [`deluge`](/Plugins/deluge) or [`transmission`](/Plugins/transmission) you may want to consider using its dedicated output plugin instead.)

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
          quality: 720p
    download:
```

Note in the above example, this is the first time we have unindented (moved the text back towards the left side of the screen). Since `download` is a plugin of its own and it doesn't belong to `series`, but rather to our `test task`, it's moved back to line up with `series` and `rss`.

The [`download`](/Plugins/download) plugin also has a simple configuration option, in which we just define the path where we would like FlexGet to save our content.

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
          quality: 720p
    download: /home/me/watchdir/
```
Congratulations! You now have a fully functioning config file. You can continue to add more tasks to your config file to complete different jobs, or customize this one further.

Remember to consult the [plugins](/Plugins) wiki page to choose your plugins, and read the individual page for each plugin to figure out how to configure that specific plugin.

**Now just sit back, and let FlexGet do the work for you!**

## Common misconceptions
 * Plugin order doesn't matter. You can list them in any order you like. The most logical order would be `inputs` > `filters` > `outputs`.
 * Task order doesn't matter. Tasks are executed in a seemingly random order. Use the  [`priority` plugin](/Plugins/priority) to prioritize tasks when necessary.
 * With very few exceptions, you cannot use plugins more than once in a single task. This is limited by the chosen simpler syntax in the configuration file. Instead, see the [`template` plugin](/Plugins/template).

## Tips
### Task Naming
Take special care when naming your tasks as this could be very helpful later on. Say you want to use a [schedule](/Daemon#Scheduling), or call several tasks in one call to do similar things. With a little thought to task naming and the use of wildcard calls, this can be very simple. This makes setting up schedules and batch task calls easy.

Take the following tasks list as an example:

```yaml
tasks:
  Series-Primary:
    #find configured series in the given inputs...
  Series-Premieres:
    #find series premieres from given inputs...
  Update-Queue:
    #update movie queue...
  Movies-Queue:
    #check for movie queued items from given inputs...
  Movies-All:
    #filtered movies based on settings given... 
  Update-trakt-TV:
    #update trakt series list using trakt_acquired...
  Update-trakt-Movies:
    #Update trakt movie list using trakt_acquired...
```

As you can see above, there are seven tasks listed, but instead of calling each task individual, or all of them at once, you could use wildcards on the command line like this:

```bash
# executes Series-Primary and Series-Premieres
$ flexget execute --tasks Series-*
$ flexget execute --tasks Update-Queue
# executes Movies-Queue and Movies-All
$ flexget execute --tasks Movies-*
# executes Update-trakt-TV and Update-trakt-Movies
$ flexget execute --tasks Update-trakt-*
```

Or setup a [schedule](/Daemon#Scheduling). The wildcards operate in the same as they do in the command line example above.

```yaml
schedules:
  - tasks: 'Update-Queue'
    interval:
      hours: 3
  - tasks: 'Series-*'
    interval:
      minutes: 30
  - tasks: 'Movies-*'
    interval:
      hours: 1
  - tasks: 'Update-trakt-*'
    interval:
      days: 1
      at_time: 4:43 am
```

### Test execution
This command executes all tasks, but doesn't write anything to the disk. Additionally, some network functionality is disabled during testing. See the [CLI `--test`](/CLI#flexget-level-arguments) argument for more details.

```cmd
$ flexget --test execute
```

### Check configuration syntax
When you create or modify your configuration file, try running FlexGet with the [`check` command](/CLI/check). It will go through the configuration file and report any irregularities or errors found. If you used the recommended configuration name and location, simply executing `flexget check` will do this. If this doesn't report any errors you should have a fully-working configuration file.

Note that it may report warnings, but these are not errors and can usually safely be ignored.

## References
 * See [how to manage series](/Cookbook/Series/Template) in the Cookbook for how to refine this example into real world usage (with multiple tasks).
 * Continue into [plugins](/Plugins) to learn about all of the available plugins you may use in the configuration file.
 
 
<div class="alert alert-info" role="alert">

Check [this](/StillConfusedYaml) if you are still confused about YAML syntax.

</div>