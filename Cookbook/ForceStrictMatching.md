= Force Exact Matching =

Certain times, when using [wiki:Plugins/configure_series configure_series] you might want to force !FlexGet into exact matching for a TV series.

== An Example ==

Say a user follows a series named Seriesname, this series is broadcasted in national versions in several countries. Thus the series that exist are:

* Seriesname
* Seriesname UK

By default !FlexGet will consider both of these series the same, if 'Seriesname' is the title provided by configure_series.

== The Workaround ==

To solve this we can manually specify [wiki:Plugins/series/exact exact] mode for this series using the regular [wiki:Plugins/series series] plugin.

{{{
# Use configure_series as normal, and also include the series plugin like this:
series:
  # The series name specified here should be exactly the same as it comes from configure_series
  - Seriesname:
      exact: yes
}}}
The exact option will be merged into this specific series, along with any options you have specified for all series using configure_series plugin.