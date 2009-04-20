= Configuration =

In order to use !FlexGet you'll need to create a configuration file. By default !FlexGet tries to find {{{config.yml}}} from it's installation directory. 

!FlexGet uses [http://en.wikipedia.org/wiki/Yaml Yaml] markup in configuration file. 

{{{
#!html
<h2 style="color: red">Common mistakes</h2>
}}}

 * Indentation level. always use '''2 spaces''' and '''never''' use tab-key
 * '''All''' modules are supposed to be indented at the same level (ie. rss, series, download etc)
 * Missing colons. Pay special attention to these when looking examples and documentation. If text value contains colon it must be "quoted".

= File structure =

Mandatory file structure has been kept minimal. Each configuration file must have structure of:

{{{
feeds:
  feed A:
    .
    .
  feed B:
    .
    .
}}}

== Feed configuration ==

This depends largely on what you're trying to accomplish. Let's assume that you're trying to download from RSS-feed. First you'll need to add [wiki:InputRSS rss] (input) module. Notice how RSS is indented by 2 spaces, this is because it belongs to a feed (or think "my feed" has "rss"). This will create items (called [wiki:Entry entries]) from entire RSS feed.

{{{
feeds:
  my feed:
    rss: http://example.com/rss
}}}

If you don't want to get everything from the RSS feed you'll need to sort out the content you're interested about. This happens trough various [wiki:Modules#Filters filters]. Most commonly [wiki:FilterPatterns patterns] module. All modules are indented at same level, in this case rss and patterns. But notice how patterns list is indented once again by 2 additional spaces. This is because the list belongs to patterns.

{{{
feeds:
  my feed:
    rss: http://example.com/rss
    patterns:
      - my.interesting.show
      - another.interesting.show
}}}

And you probably want to download the result as well, so let's throw output module [wiki:OutputDownload download] in as well.

{{{
feeds:
  my feed:
    rss: http://example.com/rss
    patterns:
      - my.interesting.show
      - another.interesting.show
    download: /home/myself/podcasts/
}}}

When you create or modify configuration try running !FlexGet with --check parameter. It will go through configuration file and report any irregularities. If you used default configuration file name simply execute {{{./flexget.py --check}}}.

If --check does not find any problems you have successfully created fully working configuration file, that wasn't so hard was it? In reality when dealing with TV-series you may wish to use [wiki:FilterSeries series] filter instead of patterns.

'''Test your configuration file:'''

{{{
./flexget.py --test
}}}

Continue into [wiki:Modules modules] to learn all about modules you may use in you configuration file.

== Still confused about Yaml? ==

Please note that each indentation level must be precisely '''2 spaces'''. Tabs are forbidden for indentation. Why are indentation even required in Yaml? It is used for semantics or '''relation'''. Consider example:

{{{
pets:
  cat:
    name: furry
    age: 5
  dog:
    name: barky
    age: 2
    toys:
      - bone
      - ball
}}}

Here we have two pets, cat and dog. Each of them has name, and age. Dog has list of toys. If we were to use more conventional configuration file format it would be much messier to represent complex relations.

Some other configuration files might represent previous example in following form:

{{{
pets.cat.name=furry
pets.cat.age=5
pets.dog.name=barky
pets.dog.age=2
pets.dog.toys=bone, ball
}}}

But consider more complex situation ...

{{{
pets:
  dog:
    name: barky
    age: 2
    toys:
      - ball:
          color: blue
          size: 70mm
      - bone:
          dimensions:
            length: 10cm
            height: 2cm
          taste: chicken
}}}

And you have nice mess in your hands ...