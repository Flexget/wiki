[[PageOutline]]
= Series =

Intelligent filter for TV-series.

=== Open defects ===

[[TicketQuery(keywords=~series, milestone=1.0, type=defect, status=assigned|reopened, compact)]]

== Features ==

 * Episode tracking, no duplicate downloads
 * Plenty of quality options
 * Timeframe, get best quality in given timeframe
 * Episode advancement
 * !Proper/Repack aware

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

Only one of them is downloaded, with default configuration best quality is chosen^1^.

'''Notes:'''

 * !FlexGet respects ''propers'' which means that the same episode will be downloaded twice if the second one contains words such as {{{proper}}}, {{{repack}}}, {{{rerip}}}, or {{{real}}}.
 * If series name is written in multiple different ways, don't add them as separate series. This will confuse episode tracking. Use the most common form and add `name_regexps` that contains all forms!

= Settings =
The series plugin supports a number of settings to customize it's behavior. All settings can be applied in either of the following formats.
==== Per series settings ====

When specifying a setting for a series, you must add a colon to the end of the series name, and add 4 more spaces before the setting name:
{{{
series:
  - series name:
      [setting]: [value]
}}}
For example, with [wiki:Plugins/series#Quality quality] settings:
{{{
series:
  - Series 1
  - Series 2:
      quality: hdtv
  - Series 3:
      quality: 720p
}}}
==== Group settings ====

Many times, you will want to apply a setting to more than one show at once. In this instance, you can use a more advanced config format, to define groups, and settings that apply to the whole group.
{{{
series:
  [settings]:
    [group name]:
      [setting]: [value]
  [group name]:
    - first series
    - second series
}}}
An example, setting [wiki:Plugins/series#Propers propers] for ''group 1'':
{{{
series:
  settings:
    group 1:
      propers: 3 days
  group 1:
    - Series 1
    - Series 2
  720p:
    - Series 3
    - Series 4:
        quality: 1080p
  normal:
    - Series 5
}}}
Notes:

 * The names of the groups are arbitrary, so you can pick whatever you want.[[BR]]
 In this example ''normal'' is just a group without any options.
 * If a group name is a quality, it will automatically have that as a quality.[[BR]]
 In this example ''Series 3'' has it's quality set to 720p, because 720p is a [wiki:Plugins/quality#KnownQualities known quality name.]
 * Series may override any settings specified in group settings.[[BR]]
 In this example ''Series 4'' overrides the quality setting of it's group with 1080p.
----
== Quality ==

||'''Name'''||'''Description'''||
||quality||Accept only given quality. No other quality will be accepted.||
||min_quality||Accept only qualities equal or above this^*^||
||max_quality||Accept only qualities equal or below this^*^||
||qualities||Accept all given qualities, multiple downloads^*^||

^* = Does not work with [#Timeframe timeframe] (but there is a [wiki:Cookbook/Series/TimeframeWithMinMaxQuality workaround])^

Possible values for quality can be found [wiki:Plugins/quality#KnownQualities here.]

'''Example:'''

{{{
series:
  - some series:
      quality: 720p
  - another series:
      min_quality: hr
      max_quality: 720p
  - third_series:
      qualities:
        - pdtv
        - 720p
}}}

Usually best way to specify quality for series is to use groups:

'''Example:'''

{{{
series:
  720p:
    - name 1
    - name 2
  hdtv:
    - name 3
    - name 4
}}}

See [wiki:Plugins/series#Groupsettings groups] for more information.

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

Timeframe value: NUM (minutes|hours|days|weeks)

== Propers ==

Default behavior is to download propers always.

To disable propers completely:

{{{
series:
  - some series:
      quality: 720p
      propers: no
}}}

To specify timeframe in which propers are accepted:

{{{
series:
  - some series:
      quality: 720p
      propers: 12 hours
}}}

Accepted format: NUM (minutes|hours|days|weeks)

== Override path ==

Specify a custom path for a series. Note that this does '''not''' download it, your feed must have output plugin (eg. [wiki:Plugins/download download], [wiki:Plugins/deluge deluge])

'''Example:'''

{{{
series:
  - some series:
      path: ~/download/some_series/
  - another series
  - third series
download: ~/download/
}}}

Series {{{another series, third series}}} will be downloaded into {{{~/downloads}}}. However {{{some series}}} has overridden path and will be downloaded into {{{~/downloads/some_series/}}}.

It's also possible to set path globally from series name with [wiki:Plugins/set set] plugin, see [wiki:Cookbook/SetPath this recipe].

== Exact mode ==

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

'''Forget...'''[[BR]]
In case you have situation where !FlexGet is downloading episodes from another series with similar name, turn on the `exact` manually. You may also need to reset the series status with `--series-forget NAME` in case wrong episodes have been downloaded and it confuses ''episode advancement''.
Forgetting single episode is also possible by `--series-forget NAME" sxxexx, where xx is season number and episode number. In case you want to add some already watched episode have a look at [wiki:Plugins/--inject --inject]. Remember only latest episode is needed.

== Specify group (eg. anime fansubs) ==

'''Example:'''

{{{
series:
  - fullmetal alchemist brotherhood:
      from_group: eclipse
  - naruto:
      from_group:
        - horriblesubs
        - crunchysubs
}}}

'''Supported notations:'''

 * [Group] Series
 * Series XviD-Group

To disallow certain groups use [wiki:Plugins/regexp regexp] plugin to reject them.

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

== Identified by ==

Specify how episode number is detected.

'''Example:'''

{{{
series:
  - test:
      identified_by: id
}}}

Possible values: `ep`, `id`, `auto`

Default value is `auto` which uses episode history to detect what to use. In absence of reliable history both `ep` and `id` format are accepted.

== Advanced matching with regexps ==

The standard name matching is not perfect, some times you may need to specify regexp(s) manually. Usually the `name_regexp`.

'''Notes:'''
 
 * Use this only if you're having problems with matching, it should be able to handle 99% of cases without any regexp tweaking.
   * `name_regepx` is useful for series which are written in more than one way
 * If specifying name_regexp(s) make sure that these match only to the given series
 * Pay attention to the ''indentation'' here

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

== Set entry fields ==

Setting this key uses the [wiki:Plugins/set set] plugin to attach some information to each entry that matches the [#Perseriessettings series] or [#Groupsettings series group]. Other plugins may use this information to override their default settings for these entries. For example here is how it might be used to set the [wiki:Plugins/deluge deluge] {{{movedone}}} option for different series groups:

{{{
series:
  settings:
    720p:
      set:
        movedone: /media/TV/HD
    hdtv:
      set:
        movedone: /media/TV/SD
  720p:
    - Good Shows
  hdtv:
    - OK Shows
}}}