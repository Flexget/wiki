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
Our input plugin will create an entry for every item that comes into the rss feed, but we still need to tell !FlexGet which of those items we want. We do this with a [wiki:Plugins#filter filter] plugin. One of the most common is the [wiki:Plugins/series series] plugin, so we will configure that here. This plugin will belong to our `test feed` so we remain at the same indentation level, 2 more spaces than `test feed`.
{{{
feeds:
  test feed:
    rss: http://mysite.com/myfeed.rss
    series:
}}}
Now we must consult the [wiki:Plugins/series series] wiki page to determine how to configure the series plugin. There are two formats the series plugin configuration can take, we will stick with the simple one in this tutorial. (eventually you may want to switch to the [wiki:Plugins/series/per_group_settings grouped format]) In the simple format, the series plugin just takes a list of the series you want. Since our last line ended with a colon, we go to the next line with 2 more spaces. Each item in our list will be at this same indentation level, and start with '- ' so:
{{{
feeds:
  test feed:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
}}}
The series plugin also allows defining options per show, which we will do with our next show.
{{{
feeds:
  test feed:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
}}}
Since we are defining options for this show, we ended the line with a colon. This normally means we define the options on the next line with 2 more spaces. There is a slight exception when defining options for a list item, in that we have to go 2 more spaces than the actual word, for a total of 4 spaces. Here we will define the `quality` option of the series plugin to only allow 720p copies of this show to be downloaded.
{{{
feeds:
  test feed:
    rss: http://mysite.com/myfeed.rss
    series:
      - My Favorite Show
      - Another Good Show:
          quality: 720p
}}}