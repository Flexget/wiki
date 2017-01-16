# Configuration
In order to use FlexGet you'll need to create a configuration file. 

FlexGet uses [Yaml](http://en.wikipedia.org/wiki/Yaml) markup in configuration file. 


<div class="alert alert-warning" role="alert">
Common mistakes, read at least these!
</div>

 * Indentation level. Always use (multiples of) **2 spaces** and **never** use tab-key!
 * Plugins are supposed to be indented at the same level (rss, series, download etc). Some plugins may allow other plugins inside of them.
 * Missing colons. Pay special attention to these when looking at the examples and documentation
 * If text value contains any of `{}[]%:` characters it must be quoted with `''`
 * If you want to pass a number as a text (ie. series *24*), value must be quoted with `''`
 * [Answers for common mistakes](/PitFalls)

### Location
By default FlexGet tries to find `config.yml` from several places in this order:
- The current path
- The virtualenv path (only if you are running FlexGet installed in a virtualenv)
- `~/.flexget/` (`C:\Users\YOURUSER\flexget\` on Windows 7, and `C:\Documents and Settings\YOURUSER\flexget\` on XP)
- `~/.config/flexget` (only on linux)
The first path containing a config file will be used. Creating the `~/.flexget/` directory and placing your `config.yml` in there is currently considered the best practice. You can also use the `-c` cli flag to manually specify a config file name/location. 

## Step by Step Configuration Tutorial
The configuration is a hierarchy constructed of various components. The main component of any config are the tasks, so we will start there.
```yaml
tasks:
```
The line ends in a colon, which means we will be defining this section on the lines following. We then indent (2 spaces) everything that belongs to this section. The tasks sections is made up of all your individual tasks, which can be named whatever we want. Let's make one called `test task`.
```yaml
tasks:
  test task:
```
This line defining the task name (test task) also ends with a colon, which means we will be defining what belongs in this task on the following lines with another indent (2 more spaces.) The contents of an individual task are always [plugins](/Plugins). There are three main types of plugins we normally want in a task, an [input](/Plugins#inputs) (where do you want FlexGet to look for things?), a [filter](/Plugins#filter) (which of those things do you want?) and an [output](/Plugins#output) (what do you want FlexGet to do with those things?). Let's start by adding an input plugin to our task, `test task`. In this case we will use the [rss](/Plugins/rss) plugin as our input. The indentation of rss is increased and means that it belongs under the test task.
```yaml
tasks:
  test task:
    rss:
```
We aren't finished yet, this line ends with a colon, which means we need to provide the next section, which would be the options for the rss plugin. When configuring any plugin, visit that plugin's [wiki page](/Plugins) to find out what format the options for that plugin should be in. The most simple configuration format for the rss plugin allows us to just define the url for the rss feed. If the plugin has more complicated configuration, follow the indentation shown in the plugin documentation. Note that if you simply copy & paste examples from documentation you must increase the indentation to correct level.

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
```

Our input plugin will create an entry for every item that comes into the rss feed, but we still need to tell FlexGet which of those items we want. We do this with a [filter](/Plugins#filter) plugin. One of the most common is the [series](/Plugins/series) plugin, so we will configure that here. This plugin will belong to our `test task` so we remain at the same indentation level, 2 more spaces than `test task`.

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
```
Now we must consult the [series](/Plugins/series) wiki page to determine how to configure the series plugin. There are two formats the series plugin configuration can take, we will stick with the simple one in this tutorial. (eventually you may want to switch to the [grouped format](/Plugins/series/per_group_settings)) In the simple format, the series plugin just takes a list of the series you want. Since our last line ended with a colon, we go to the next line with 2 more spaces. Each item in our list will be at this same indentation level, and start with '- ' so:

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
Since we are defining options for this show, we ended the line with a colon. This normally means we define the options on the next line with 2 more spaces. There is a slight exception when defining options for a list item, in that we have to go 2 more spaces than the actual word, for a total of 4 spaces. Here we will define the `quality` option of the series plugin to only allow 720p copies of this show to be downloaded.

```yaml
tasks:
  test task:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
          quality: 720p
```
Now that we have an input and a filter plugin, we need to tell FlexGet what we want to do with the entries that are accepted by our filter. We do this with an [output plugin](/Plugins#output). One common output plugin is the [download](/Plugins/download) plugin, which we could use to save our items to a watch directory from a bittorrent or nzb client. (if you are using [deluge](/Plugins/deluge) or [transmission](/Plugins/transmission) you may want to consider using its dedicated output plugin instead)

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
The [download](/Plugins/download) plugin also has a very simple configuration option, in which we can just define the path where we would like it to save our content.

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
Congratulations, we now have a fully functioning config file. You can continue to add more tasks to your config file to complete different jobs, or customize this one further. Remember to consult the [plugins](/Plugins) wiki page to choose your plugins, and read the individual page for each plugin to figure out how to configure that specific plugin.

**Now just sit back, and let FlexGet do the work for you! **
## Common misconceptions
 * Plugin order doesn't matter, you can list them in any order you like. Most logical order would be `inputs` -> `filters` -> `outputs`.
 * Task order doesn't matter, tasks are executed in seemingly random order. Use [priority](/Plugins/priority) plugin priorize tasks when necessary.
 * You cannot list plugins, ie. [rss](/Plugins/rss) twice in a single task. This is limited by the chosen simpler syntax in the configuration file. Instead see [template](/Plugins/template) plugin.

## Tips
### Task Naming
Take special care when naming your tasks, as this could be very helpful later on. Say you want to use a [schedule](/Daemon#Scheduling), or call several tasks in one call to do similar things. With a little thought to task naming and the use of wildcard calls, this can be very simple. This makes setting up schedules and batch task calls easy.

Take the following tasks list as an example:

```yaml
tasks:
  Series-Primary:
    #find configured series in the given inputs..
  Series-Premieres:
    #find series premieres from given inputs..
  Update-Queue:
    #update movie queue...
  Movies-Queue:
    #check for movie queued items from given inputs..
  Movies-All:
    #filtered movies based on settings given... 
  Update-trakt-TV:
    #update trakt series list using trakt_acquired..
  Update-trakt-Movies:
    #Update trakt movie list using trakt_acquired...
```

As you can see above, there are seven (7) tasks listed, but instead of calling each task individual, or all of them at once, you could make calls like this:

```yaml
flexget execute --tasks Series-*
flexget execute --tasks Update-Queue
flexget execute --tasks Movies-*
flexget execute --tasks Update-trakt-*
```

or setup a [schedule](/Daemon#Scheduling):

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
Executes all tasks, but doesn't write anything into disk.

```cmd
$ flexget --test execute
```

### Display more process details
Adding `-v` parameter will display useful information about task(s) content.

### Check configuration syntax
When you create or modify configuration try running FlexGet with `check` parameter. It will go through the configuration file and report any irregularities found. If you used recommended configuration name and location, simply executing `flexget check` will do this. If this doesn't report any problems you should have fully working configuration file.

## References
 * See [how to manage series](/Cookbook/Series/Template) for how to refine this example into real world usage (with multiple tasks).
 * Continue into [plugins](/Plugins) to learn all about available plugins you may use in you configuration file.
 
 
<div class="alert alert-info" role="alert">

Check [this](/StillConfusedYaml) if you are still confused about YAML syntax

</div>