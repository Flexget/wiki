[[PageOutline]]
= Series =

'''Upcoming 1.0 (under construction)'''

Intelligent filter for TV-series.

== Features ==

 * Episode tracking, no duplicate downloads
 * Quality aware
 * Timeframe, get best quality in given timeframe
 * Episode advancement

'''Simple configuration:'''

{{{
series:
  - some series
  - another series
}}}

If {{{some series}}} and {{{another series}}} have understandable episode
numbering any given episode is downloaded only once. !FlexGet should support all known episode numbering schemes without any configuration, including dates.

So if we get same episode twice:

Some.Series.S2E10.More.Text[[BR]]
Some.Series.S2E10.Something.Else

Only one of them is downloaded, with default configuration best quality is chosen.

'''Notes:'''

 * Configured series name should not contain anything else than a series name. This is because if you change or reformat name !FlexGet will lose track of already downloaded episodes.

== Episode advancement ==

By default series plugin keeps track of downloaded episodes for each series and rejects episodes that are too far in the past. Small margin from latest episode is allowed.

'''Example:'''
Series Chuck latest episode is S02E22 and suddenly a feed contains S01E01 which series plugin has not seen or downloaded.[[BR]]
'''Result:'''
Episode advancement rejects this episode since it's too far in the past.

'''Example:'''
Series Chuck latest episode is S02E22 and suddenly a feed contains S02E20 which series plugin has not seen or downloaded.[[BR]]
'''Result:'''
Episode advancement does not reject this.

== Group settings ==

''Todo: write userfriendly ''

{{{
series:
  [settings]:
    [group]:
      [setting]: [value]
  [group]:
    - first series
    - second series
}}}

Series may override any settings specified in group settings.

'''Example:'''

{{{
series:
  settings:
    720p:
      timeframe: 12 hours
      quality: 720p

  720p:
    - series name
  normal:
    - another series
}}}

There is convenience feature built in. If a group name is a known quality, it will automatically generate a settings with that quality.

'''Example:'''

{{{
series:
  720p:
    - series name
  normal:
    - another series
}}}

This is same as previous example except without timeframe.

== Quality ==

Accept only when given quality becomes available.

'''Example:'''

{{{
series:
  - some series:
      quality: 720p
  - another series
  - third series
}}}

== Timeframe ==

Specify a timeframe in which !FlexGet waits for best quality. If optional quality is given, this is considered to be satisfactory and proceeded without waiting entire timeframe. If specified quality does not come available within timeframe best quality so far is chosen.

'''Example:'''

{{{
series:
  - some series:
      timeframe: 4 hours
      quality: 720p
  - another series
  - third series
}}}

Possible values for quality (in order): 1080p, 1080, 720p, 720, hr, dvd, hdtv, pdtv, dsr, dsrip

== Override path ==

Specify a custom path for a series. Note that this does '''not''' download it, your feed must use [wiki:OutputDownload download] plugin to do that.

'''Example:'''

{{{
series:
  - some series:
      path: ~/download/some_series/
  - another series
  - third series
download: ~/download/
}}}

Series {{{another series, third series}}} will be downloaded into {{{~/downloads}}}. However {{{some series}}} has overriden path and will be downloaded into {{{~/downloads/some_series/}}}.

'''Example with timeframe:'''

{{{
series:
  - some series:
      timeframe: 4 hours
      quality: 720p
      path: ~/download/some_series/
  - another series
  - third series
download: ~/download/
}}}

== Advanced matching with regexps ==

The standard name matching is not perfect, if you're used to working with regexps you can
specify regexp(s) that filter for the show's name, episode number or unique identifier. (See ticket #323).

'''Note:''' Use this only if you're having problems with matching, it should be able to handle 99% of cases without any regexp tweaking.

'''Example:'''

{{{
series:
  - some series:
      name_regexp: ^some.series
      ep_regexp: (\d\d)-(\d\d\d)  # must return TWO groups, both being numeric values
      id_regexp: (\d\d\d)         # can return any number of groups
  - another series
  - third series
}}}

All above regexps also accept multiple regular expressions in list form.

{{{
name_regexp:
  - ^some.series
  - ^something.entirely.different
}}}

ep_regexp is for series enumerated by season and episode numbers (eg, S04E01).  The default episode regular expressions used are

{{{
ep_regexp:
  - s(\d+)e(\d+)
  - s(\d+)ep(\d+)
  - s(\d+).e(\d+)
  - [^\d]([\d]{1,2})[\s]?x[\s]?(\d+)
}}}

id_regexp is for series that are not enumerated by season/episode numbering.

{{{
id_regexp:
 - (\d\d\d\d).(\d+).(\d+)
 - (\d+).(\d+).(\d\d\d\d)
 - (\d\d\d\d)x(\d+)\.(\d+)
 - [^s^\d](\d{1,3})[^p^\d]
}}}

User defined regexps takes priority over the built-in expressions.