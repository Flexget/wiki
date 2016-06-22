= Generic series features =

'''GOAL:''' Extract nice functionalities like timeframe, quality upgrades etc into separate plugins that can be re-used with movies.

'''Feature prospects'''

* Timeframe
* Propers
* Qualities

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
accepted = plugin.get_plugin_by_name('timeframe').instance.evaluate(
    entry, "{0} {1}".format(series_name, series_id, timeframe_config)
}}}


Same approach would be used for all features. Some of the plugins would need to keep track of entries internally. Currently a backlog plugin is used to keep items in the task until timeframe for example does it's thing.

Ps. As an addition to timeframe I would like to set "deadline" for series, get something regardless of the quality before certain time.

=== Generic use in task ===

This could be used in task standalone

{{{
timeframe:
  identified_by: {{ series_name }} {{ series_id }}
  target: 720p
}}}


=== Standalone with movies ===

{{{
rss: .....
imdb_lookup: yes
timeframe: 
  amount: 12h
  target: 720p
  identified_by: {{ imdb_id }}
imdb:
  min_score: 6.5
}}}
 
'''NOTES:''' 

* I hate how identified_by NEEDS to use jinja2 formatting, it makes no sense for enduser
* Timeframe needs to operate on accepted entries in order to work well with other plugins

=== With new movies plugin ===

{{{
rss: ....
movies:
  from:
    - movie_list: movies
  timeframe:
    amount: 12h
    target: 720p
}}}

'''NOTES:''' 

* movies plugin will need to supply identified_by to timeframe somehow
* does movies plugin bring anything here opposed to

{{{
rss: ...
imdb_lookup: yes
list_match:
  from:
    - movie_list: movies
timeframe:
  identified_by: {{ imdb_id }}
  amount: 12h
  target: 720p
}}}

== identified_by ==

Maybe we can get rid of having to specify identified_by manually by providing some facilities for that.

Issue comes down to now knowing which fields are id fields and which are not. Possible solutions:

'''Option 1'''

{{{
entry['ids'] = ['imdb_id', 'tmdb_id']
}}}

appended by imdb_lookup etc


'''Option 2'''

Use type

{{{
class Identity:
  
   def __init__(self, name, value):
     self.name = name
     self.value = value
}}}

usage:

{{{
entry['imdb_id'] = Identity('imdb', 123)

isinstance(ntry['imdb_id'], Identity)
}}}

=== Problem ===

What if we have multiple ids .. which one we put into "identified_by" ? In fact whole identified_by parameter becomes unnecessary if we have ids in the entry.

What about more complex ids? Like with episodes, to determine if they are the same thing, we might have to check if the current entry has equal: `'trakt_episode_id' or (('trakt_series_id' or 'imdb_id' or ('series_name' and 'series_year')) and 'series_id')`

=== Example flow (Quality) ===

Assuming we are using multiple ids and each id field is an identifier class. 

{{{
rss: .....
imdb_lookup: yes
tvdb_lookup: yes
quality:
  upgrade: true
  accept:
    - 720p hdtv
    - 1080p webdl
regex:
  accept:
      - Game Of Thrones
}}}
 
Identifers set by meta plugins

- Identifer(name='tvdb_id', value='123456')
- Identifer(name='imdb_id', value='123456')
- Identifer(name='series_id', value='S01E01', required=True)

First run (Game.Of.Thrones.S01E01.HDTV)
1. Quality looks for existing (not found)
2. Regex accepts
3. Quality plugin stores accepts in db.. Not sure how yet


Second run (Game.Of.Thrones.S01E01.720p)
1.
2.
3.

== A different possibility ==
EDIT: Perhaps this section is not good. I failed to fully understand paranoidi's idea until now, and I think that's better. Rather than trying to make different plugins content aware, just factor out the content aware features into a utility that already content aware plugins can then use.

Instead of making plugins like quality have to be aware of the content id, a separate plugin that works like the 'timeframe' suite in series plugin, but let you use any unique content unaware filters.

I don't like timeframe as the name of this, but keeping for examples sake:
{{{
timeframe:
  target:
    quality: 1080p  # This is still just the normal quality filter plugin
    regexp:
      reject:
        - screener
  1 hour:
    quality: 720p
}}}

The timeframe plugin would keep track of content ids for all previously seen entries. For every entry in the task, it would check its database to see if a release for that content has been seen before, it would apply the appropriate plugins from the different timed sections of config based on the first seen entry time, and reject outright if we've already accepted an entry for that content id. The plugin could also keep track of what 'section' ('target', '1 hour', etc.) was active when things got accepted, to allow for an 'upgrade' behavior. i.e. imdb_id xxx was accepted with the '1 hour' filters activated, if upgrade mode is enabled, it'd still look until it got a copy that passed the 'target' filters.