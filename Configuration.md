= Configuration =

In order to execute !FlexGet you will need to write configuration file. The default name which !FlexGet tries to find is {{{default.yml}}}. If you use multiple files or different name you must specify configuration file via -c parameter.

!FlexGet uses [http://en.wikipedia.org/wiki/Yaml Yaml] markup in configuration file. You can find [wiki:YamlTutorial here] minimal Yaml tutorial.

= File structure =

Mandatory file structure has been kept minimal. Each configuration file must have structure of:

{{{
feeds:
  <feed name>:
    <feed configuration here>
}}}


== Feed configuration ==

Well that really depends on what you're trying to accomplish. For example if you're trying to get stuff out from RSS-feed you'll need to add [wiki:InputRSS rss] module.

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

Continue into [wiki:Modules modules] to learn all about modules you may use in you configuration file.