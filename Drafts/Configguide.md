== Basic Configuration Layout and Overview ==
The configuration is a hierarchy constructed of various components. The main component of any config are the feeds, so we will start there.
{{{
feeds:
}}}
The line ends in a colon, which means we will be defining this section on the lines following. We then indent (2 spaces) everything that belongs to this section. The feeds sections is made up of all your individual feeds, which can be named whatever we want. Let's make one called `test feed`.
{{{
feeds:
  test feed:
}}}
This line also ends with a colon, which means we will be defining what belongs in this feed on the following lines, with another indent (2 more spaces.) The contents of an individual feed are always [wiki:Plugins plugins]. There are three main types of plugins we normally want in a feed, an [wiki:Plugins#inputs input] (where do you want !FlexGet to look for things?), a [wiki:Plugins#filter filter] (which of those things do you want?) and an [wiki:Plugins#output output] (what do you want !FlexGet to do with those things?). Let's start by adding an input plugin to our feed, `test feed`. In this case we will use the [wiki:Plugins/rss rss] plugin as our input.
{{{
feeds:
  test feed:
    rss:
}}}
We aren't finished yet, this line ends with a colon, which means we need to provide the next section, which would be the options for the rss plugin. When configuring any plugin, visit that plugin's [wiki:Plugins wiki page] to find out what format the options for that plugin should be in. The most simple configuration format for the rss plugin allows us to just define the url for the rss feed.
{{{
feeds:
  test feed:
    rss: http://mysite.com/myfeed.rss
}}}
