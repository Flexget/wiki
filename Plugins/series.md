= Series =

Intelligent filter for TV-series.

== Features ==

 * Episode tracking, no duplicate downloads
 * Plenty of [wiki:Plugins/series/quality quality] options
 * [wiki:Plugins/series/timeframe Timeframe], get best quality in given timeframe
 * Episode [wiki:Plugins/series/advancement advancement] (for season, episode).
 * [wiki:Plugins/series/propers Proper & Repack] aware
 * Specials aware (grabs episodes with the series title and the word 'special')
 * Tries to ignore season packs, you can use [wiki:Plugins/content_size content_size] for extra insurance against them.
 * Supports double episodes. i.e. S01E01-E02

'''Simple configuration:'''

{{{
series:
  - some series
  - another series
}}}

If {{{some series}}} and {{{another series}}} have understandable episode
numbering any given episode is downloaded only once. !FlexGet should support all known episode numbering schemes without any configuration, including dates.

So if we get same episode twice:

 * Some.Series.S2E10.720p.x264-!FlexGet
 * Some.Series.S2E10.HR.x264-!FooBar

Only one of them is downloaded, with default configuration best quality is chosen.

== Related plugins ==

These plugins are complementary to the series plugin.

 * [wiki:Plugins/all_series all_series] - Grab all series in the feed
 * [wiki:Plugins/import_series import_series] - Automatically configures series by using another input, some examples:
   * [wiki:Plugins/thetvdb_favorites thetvdb_favorites] - [http://thetvdb.com TheTVDB.com] favorites
   * [wiki:Plugins/trakt_list trakt_list] - [http://trakt.tv Trakt.tv] lists
   * [wiki:Plugins/listdir listdir] - You local directory listing
 * [wiki:Plugins/series_premiere series_premiere] - Download all premieres

== Settings ==

The series plugin supports a number of settings to customize it's behavior.

||'''Option'''||'''Description'''||
||[wiki:Plugins/series/quality quality]||Required quality.||
||[wiki:Plugins/series/qualities qualities]||Download all listed qualities when they become available.||
||[wiki:Plugins/series/upgrade upgrade]||Keeps getting the better qualities as they become available.||
||[wiki:Plugins/series/timeframe timeframe]||Wait given amount of time for specified quality to become available, after that fall back to best so far.||
||[wiki:Plugins/series/timeframe enough]||An acceptable quality that should be downloaded without waiting for {{{timeframe}}} to complete.||
||[wiki:Plugins/series/path path]||Set ''path'' field for this series.||
||[wiki:Plugins/series/set set]||Use [wiki:Plugins/set set] plugin to set any fields for this series.||
||[wiki:Plugins/series/exact exact]||Configure exact matching behavior. Needed for series which have similar named series. Uses 'auto' mode as default.||
||[wiki:Plugins/series/from_groups from_groups]||Accept series only from given groups.||
||[wiki:Plugins/series/identified_by identified_by]||Configure how episode numbering is detected. Uses 'auto' mode as default.||
||[wiki:Plugins/series/propers propers]||Configure how propers are handled.||
||[wiki:Plugins/series/specials specials]||Turn off specials support for series. (on by default)||
||[wiki:Plugins/series/watched watched]||Manually specify minimum season and episode from where to continue.||
||[wiki:Plugins/series/regexps name_regexp]||Manually specify regexp(s) that matches to series name.||
||[wiki:Plugins/series/regexps#Episodenumberingmatching ep_regexp]||Manually specify regexp(s) that matches to episode, season numbering.||
||[wiki:Plugins/series/regexps#Episodenumberingmatching id_regexp]||Manually specify regexp(s) that matches to series identifier (numbering).||

All settings can be applied in either of the formats.

[wiki:Plugins/series/per_series_settings How to configure settings per series][[BR]]
[wiki:Plugins/series/per_group_settings How to configure settings with groups]

== Notes ==

 * If the series appears in feed(s) with slightly different naming conventions and spinoffs like !FooBar and !FooBar US read [wiki:Plugins/series/closematch this guide]. 
 * !FlexGet respects ''propers'' which means that the same episode will be downloaded twice if the second one contains words such as {{{proper}}}, {{{repack}}}, {{{rerip}}}, or {{{real}}}.
 * If series name is written in multiple different ways, don't add them as separate series. This will confuse episode tracking. 
 * Check [wiki:Cookbook/Series series cookbook] for more complete examples and advanced uses.

== Commandline Arguments ==

The series plugin provides following commandline arguments.

=== --series ===

Display series summary. To get more details from any listed series you can use --series <name>.

=== --series-forget ===

Delete episodes from database or whole series completely.

To delete single episode, use:

--series-forget <name> <id>

To delete whole series, use:

--series-forget <name>

=== --disable-advancement ===

If episode advancement is causing problems downloading latest episode due large gap in the series history, you can use this option to disable advancement enforcement temporarily.

=== --stop-waiting ===

Stops timeframe for given name, thus downloading any episode that is currently pending in the timeframe.