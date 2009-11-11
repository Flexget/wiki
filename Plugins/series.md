[[PageOutline]]
= Series =

Intelligent filter for TV-series.

== Features ==

 * Episode tracking, no duplicate downloads
 * Quality aware
 * Timeframe, get best quality in given timeframe
 * Episode advancement
 * Proper/Repack aware

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

Series plugin keeps track of downloaded episodes for each series and rejects episodes that are too far in the past. Small margin from latest episode is allowed.

'''Example:'''
Series Chuck latest episode is S02E22 and suddenly a feed contains S01E01 which series plugin has not seen or downloaded.[[BR]]
'''Result:'''
Episode advancement rejects this episode since it's too far in the past.

'''Example:'''
Series Chuck latest episode is S02E22 and suddenly a feed contains S02E20 which series plugin has not seen or downloaded.[[BR]]
'''Result:'''
Episode advancement does not reject this. This fits inside grace margin from latest episode.

== Quality ==

Accept only given quality. No other quality will be accepted.

'''Example:'''

{{{
series:
  - some series:
      quality: 720p
  - another series
  - third series
}}}

== Minimum and maximum quality ==

Accept any quality between given range.

'''Example:'''

{{{
series:
  - some series:
      min_quality: hr
      max_quality: 720p
  - another series
  - third series
}}}


'''Notes:''' 

 * Not (yet) compatible with timeframe


== Download multiple qualities ==

Download all given qualities.

'''Example'''

{{{
series:
  - some series:
      qualities: 
        - 720p
        - pdtv
}}}

'''Notes:''' 

 * This functionality may be later merged with quality
 * Not (yet) compatible with timeframe

== Timeframe ==

Specify a timeframe in which !FlexGet waits for a chosen quality. The desired quality can be given with `quality` directive. If specified quality does not come available within timeframe best quality so far is chosen. `Quality` has default value of 720p.

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

== Exact ==

Enable strict name matching. Useful for series which name start similarly.

'''Example'''

{{{
series:
  - Test:
      exact: yes
  - ABC
  - ABC LA
}}}

Enabling `exact` changes the mechanism so that the series name must be immediately followed by the episode number. With previous example ie. `Test Bar S01E01` would not be considered valid `Test`.

Series plugin will also auto enable exact matching if it detects that there are series configured which need it in order not to be confused with each others. In the example series `ABC` would auto-enable exact matching since that name can be confused to `ABC LA`.

In case you have situation where !FlexGet is downloading episodes from another series with similar name, turn on the `exact` manually. You may also need to reset the series status with `--series-forget NAME` in case wrong episodes have been downloaded and it confuses ''episode advancement''.

== Advanced matching with regexps ==

The standard name matching is not perfect, if you're used to working with regexps you can specify regexp(s) that for the show's name, episode number or unique identifier.

'''Notes:'''
 
 * Use this only if you're having problems with matching, it should be able to handle 99% of cases without any regexp tweaking.
 * If specifying name_regexp(s) make sure that these match only to the given series which they are beneath.

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

For example if `some series` appears in two different naming conventions, you can:

{{{
- some series:
    name_regexp:
      - ^some.series
      - ^some.srs
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

Specifying `ep_regexp` disables all `id_regexp`'s and vice versa.