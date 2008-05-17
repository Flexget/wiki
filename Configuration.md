= Configuration =

In order to execute !FlexGet you will need to write configuration file. By default !FlexGet tries to find {{{config.yml}}} from it's installation directory. In case if you decide to use other filename, path or wish to use multiple different configuration files you must specify configuration file via -c parameter. If file is in installation directory you don't need to give full path.

!FlexGet uses [http://en.wikipedia.org/wiki/Yaml Yaml] markup in configuration file. You can find minimal Yaml tutorial [wiki:YamlTutorial here].

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

Depends on what you're trying to accomplish. For example if you're trying to get stuff out from RSS-feed you'll need to add [wiki:InputRSS rss] module.

{{{
feeds:
  my feed:
    rss: <url of rss>
}}}

And if you don't want to get everything, you'll need to filter out the content you're interested about. This happens trough various [wiki:Modules#Filters filters]. Most commonly [wiki:FilterPatterns patterns] module.

{{{
feeds:
  my feed:
    rss: <url of rss>
    patterns:
      - my.interesting.show
}}}

And you probably want to download the file as well, so let's throw [wiki:OutputDownload download] module in as well.

{{{
feeds:
  my feed:
    rss: <url of rss>
    patterns:
      - my.interesting.show
    download: /home/myself/podcasts/
}}}

There you have fully working configuration file, that wasn't so hard was it? :)

Continue into [wiki:Modules modules] to learn all about modules you may use in you configuration file.