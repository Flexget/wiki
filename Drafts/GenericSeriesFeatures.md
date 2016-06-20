= Generic series features =

'''GOAL:''' Extract nice functionalities like timeframe, quality upgrades etc into separate plugins that can be re-used with movies.

Disclaimer: Some of this might not be applicable, it has been long time since I've done anything to the codebase.

Each of these sub-functions could be separate plugins/services. Let's think timeframe for example.


{{{
class Timeframe:
  def evaluate(self, entry, identified_by, config):
     .
     .
     # return None or entry that should be accepted
}}}


Example usage from series_plugin

{{{
accepted = plugin.get_plugin_by_name('timeframe').instance.evaluate(entry, "{0} {1}".format(series_name, series_id, timeframe_config)
}}}


Same approach would be used for quality, upgrade etc. Some of the plugins would need to keep track of entries internally. Currently a backlog plugin is used to keep items in the task until timeframe for example does it's thing.

Ps. As an addition to timeframe I would like to set "deadline" for series, get something regardless of the quality before certain time.