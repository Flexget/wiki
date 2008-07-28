= Configuration =

In order to execute !FlexGet you will need to create a configuration file. By default !FlexGet tries to find {{{config.yml}}} from it's installation directory. In case if you decide to use other filename, path or wish to use multiple different configuration files you must specify configuration file via -c parameter. If file is in installation directory you don't need to give full path.

!FlexGet uses [http://en.wikipedia.org/wiki/Yaml Yaml] markup in configuration file. 

= File structure =

Mandatory file structure has been kept minimal. Each configuration file must have structure of:

{{{
feeds:
  <feed name>:
    <feed configuration here>
    .
    .
}}}

== Feed configuration ==

Depends on what you're trying to accomplish. For example if you're trying to get stuff out from RSS-feed you'll need to add [wiki:InputRSS rss] module. Note that since all modules are given for a feed, they must always be indented by 2 spaces from feed name.

{{{
feeds:
  my feed:
    rss: <url for rss>
}}}

And if you don't want to get everything, you'll need to filter out the content you're interested about. This happens trough various [wiki:Modules#Filters filters]. Most commonly [wiki:FilterPatterns patterns] module. Notice how patterns parameters are indented once again by 2 additional spaces. This is because they belong to key patterns.

{{{
feeds:
  my feed:
    rss: <url of rss>
    patterns:
      - my.interesting.show
      - another.interesting.show
}}}

And you probably want to download the file as well, so let's throw [wiki:OutputDownload download] module in as well.

{{{
feeds:
  my feed:
    rss: <url of rss>
    patterns:
      - my.interesting.show
      - another.interesting.show
    download: /home/myself/podcasts/
}}}

When you create or modify configuration try running !FlexGet with --check parameter. It will go trough configuration file and report any irregularities. If you used default configuration file name simply execute {{{./flexget.py --check}}}.

If --check does not find any problems you have successfully created fully working configuration file, that wasn't so hard was it? In reality you may wish to use [wiki:FilterSeries series] filter instead of patterns.

Continue into [wiki:Modules modules] to learn all about modules you may use in you configuration file. You can also [wiki:Install#Manualexecution execute your configuration file] now.

== Still confused about Yaml? ==

Please note that each indentation level in given documentation is required and must be precisely '''2 spaces'''. Tabs are forbidden for indentation. Why are spaces even required in Yaml? They are used for semantics, consider example:

{{{
pets:
  cat:
    name: furry
    age: 5
  dog:
    name: barks a lot
    age: 2
    toys:
      - bone
      - ball
}}}

Here we have two pets, cat and dog. Each of them has name, and age. Dog has list of toys. If we were to use more conventional configuration file format it would be much messier to represent item relations.