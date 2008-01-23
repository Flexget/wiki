= Configuration =

In order to execute !FlexGet you will need to write configuration file. The default name which !FlexGet checks is {{{default.yml}}} but you can have multiple files and different name. Specify configuration file via -c parameter if you're using anything else than {{{default.yml}}}.

!FlexGet uses [http://en.wikipedia.org/wiki/Yaml Yaml] in configuration file. Quick tutorial about Yaml.

=== Key : Value ===

{{{
key: value
}}}

=== Lists ===

{{{
- value 1
- value 2
- value 3
}}}

=== Indentation counts ===

{{{
key 1: value 1
key 2: value 2
key 3: value 3
}}}

{{{
key 1:
  key 2: value 2
  key 3: value 3
}}}

What's the difference? In last {{{key 1}}} has values {{{key 2}}} and {{{key 3}}}

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