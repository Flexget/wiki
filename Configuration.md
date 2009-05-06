= Configuration =

In order to use !FlexGet you'll need to create a configuration file. By default !FlexGet tries to find {{{config.yml}}} from it's installation directory. 

!FlexGet uses [http://en.wikipedia.org/wiki/Yaml Yaml] markup in configuration file. 

{{{
#!html
<h2 style="color: red">Common mistakes, read at least these!</h2>
}}}

 * Indentation level. Always use '''2 spaces''' and '''never''' use tab-key!
 * '''All''' plugins are supposed to be indented at the same level (rss, series, download etc)
 * Missing colons. Pay special attention to these when looking examples and documentation. If text value contains colon it must be "quoted".

== Example ==

Here is our example configuration:

{{{
feeds:
  tv-shows:
    rss: http://example.com/rss.xml
    series:
      - chuck
      - southpark
    download: ~/torrents/
}}}

Now let's break that down line by line.

First line is a container which may contain any number of feeds, in our example there is only one feed called {{{tv-shows}}}, which is defined in the next line. The feed name must be indented by 2 spaces because it belongs to feeds. In Yaml relations are represented by indentation level.

=== Plugins ===

Our feed {{{tv-shows}}} has three plugins: [wiki:InputRSS rss], [wiki:FilterSeries series], [wiki:OutputDownload download]. Notice all plugins again indented by additional 2 spaces. This is because they belong to the feed {{{tv-shows}}}. In correct configuration file all plugin keywords appear in the same level.

=== Plugin: RSS ===

This is our input plugin which reads RSS-feed and produces processable [wiki:Entry entries]. From plugin [wiki:InputRSS rss] documentation we learn that it accepts URL as a parameter in it's simplest form.

=== Plugin: Series ===

This plugin expects a list of series names as a parameter. Notice again how the list is intended by 2 spaces more than series keyword. The list belongs to series plugin. This filters [wiki:Entry entries], it goes trough all of them and accepts those which match to our interest and reject rest of them.

=== Plugin: Download ===

The process ends at output, in this case we have single output that just downloads all accepted entries into given path.

== Tips ==

When you create or modify configuration try running !FlexGet with --check parameter. It will go through configuration file and report any irregularities. If you used default configuration file name simply execute {{{./flexget.py --check}}}. If this doesn't report any problems you should have fully working configuration file.

'''Test your configuration file:'''

{{{
./flexget.py --test
}}}

Continue into [wiki:Modules plugins] to learn all about available plugins you may use in you configuration file.

[wiki:StillConfusedYaml Still confused about Yaml syntax]