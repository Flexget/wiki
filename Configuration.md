= Configuration =

In order to use !FlexGet you'll need to create a configuration file. 

!FlexGet uses [http://en.wikipedia.org/wiki/Yaml Yaml] markup in configuration file. 

{{{
#!html
<h2 style="color: red">Common mistakes, read at least these!</h2>
}}}

 * Indentation level. Always use (multiples of) '''2 spaces''' and '''never''' use tab-key!
 * '''All''' plugins are supposed to be indented at the same level (rss, series, download etc)
 * Missing colons. Pay special attention to these when looking at the examples and documentation
 * If text value contains any of `{}[]%:` characters it must be quoted with `''`
 * If you want to pass a number as a text (ie. series ''24''), value must be quoted with `''`

=== Location ===

By default !FlexGet tries to find `config.yml` from current path and in `~/.flexget/`. Creating the `~/.flexget/` directory and placing your `config.yml` in there is considered currently as the best practice.

== Example ==

Here is our example configuration:

`~/.flexget/config.yml`

{{{
feeds:
  tv-shows:
    rss: http://example.com/rss.xml
    series:
      - chuck
      - south park
    download: ~/torrents/
}}}

Now let's break that down line by line.

In first line `feeds` is a container which may contain any number of feeds under it. In our example there is only one feed called `tv-shows`. The feed name must be indented by 2 spaces because it belongs to `feeds`. In Yaml relations are represented by indentation level. Pay special attention to `:` - characters.

=== Plugins ===

Our feed `tv-shows` has three plugins: [wiki:Plugins/rss rss], [wiki:Plugins/series series], [wiki:Plugins/download download]. Notice all plugins again indented by additional 2 spaces. This is because they belong to the feed `tv-shows`. In correct configuration file all plugin keywords appear in the same level.

=== Plugin: RSS ===

This is our input plugin which reads RSS-feed and produces processable [wiki:Entry entries]. By lookign at plugin [wiki:Plugins/rss rss] documentation we learn that it accepts URL as a parameter in it's simplest form.

=== Plugin: Series ===

This plugin expects a list of series names as a parameter. Notice again how the list is intended by 2 spaces more than series keyword. The list belongs to series plugin. This filters [wiki:Entry entries], it goes trough all of them and accepts those which match to our interest.

=== Plugin: Download ===

The process ends at output, in this case we have single output that just downloads all accepted entries into given path.

== Common misconceptions ==

 * Plugin order doesn't matter, you can list them in any order you like. Most logical order would be `inputs` -> `filters` -> `outputs`.
 * Feed order doesn't matter, feeds are executed in seemingly random order. Use [wiki:Plugins/priority priority] plugin priorize feeds when necessary.
 * You cannot list plugins, ie. [wiki:Plugins/rss rss] twice in a single feed. This is limited by the chosen simpler syntax in the configuration file. Instead see [wiki:Plugins/preset preset] plugin.

== Tips ==

=== Test execution ===

Executes all feeds, but doesn't write anything into disk.

{{{
flexget --test
}}}

=== Display more process details ===

Adding `-v` parameter will display really useful information about feed(s) content and filtering rules that are applied.

=== Check configuration syntax ===

When you create or modify configuration try running !FlexGet with `--check` parameter. It will go through the configuration file and report any irregularities found. If you used recommended configuration name and location, simply executing `flexget --check` will do this. If this doesn't report any problems you should have fully working configuration file.

== References ==

 * See [wiki:Cookbook/Series/Preset how to manage series] for how to refine this example into real world usage (with multiple feeds).
 * Continue into [wiki:Plugins plugins] to learn all about available plugins you may use in you configuration file.
 * [wiki:StillConfusedYaml Still confused about Yaml syntax?]