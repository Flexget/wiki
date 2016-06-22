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


=== Plugins to do ? ===
	
{{{
timeframe:
  target: 720p
  amount: 12h
}}}  
 
{{{
deadline: 
 target: 720p
 amount: 12 hours
}}}

{{{
propers: 12 hours
}}}

{{{
qualities:
  - 720p
  - 1080p
}}}	

not so sure about this ....

{{{
upgrade:
  quality:
    - 720p
    - 1080p
  group:
    - FlexGet
    - Shit
}}}	


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

== Identification mess ==

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
isinstance(entry['imdb_id'], Identity)
}}}

'''Option 3 (CURRENTLY PREFERRED)'''

New metainfo plugin, replaces all imdb_lookup, tmdb_lookup plugins etc. Each "metainfo provider" plugin would have a method which returns field name which contains the unique identifier it provides. So for `plugin.get_plugin_by_name('imdb').instance.identified_by()` would return `imdb_id`.

Usage in a task:

{{{
metainfo: imdb
}}}

Usage with movies:

{{{
rss: ....
movies:
  from:
    - movie_list: movies
  metainfo: imdb # applies to rss AND movies_list
  qualities: 
    - 720p
    - 1080p
}}}

Plugin `movie_list` produced entries contains id field(s) that were available at that time so those entries do not necessarily need to be looked up at all!


'''NOTES'''
* Imdb and tmdb plugins already provide this type of field via 'movie_metainfo' group and method 'movie_identifier'. But this applies only for movies ...
* movies_list produces entries with id field (eg. imdb_id) which movie plugin can detect as that field is known id field, it could do relevant lookup solely based on that


=== Problem ===

What if we have multiple ids .. which one we put into "identified_by" ? In fact whole identified_by parameter becomes unnecessary if we have ids in the entry.

What about more complex ids? Like with episodes, to determine if they are the same thing, we might have to check if the current entry has equal: `'trakt_episode_id' or (('trakt_series_id' or 'imdb_id' or ('series_name' and 'series_year')) and 'series_id')`

=== Example flow (Quality) ===

Assuming we are using multiple ids and each id field is an identifier class. 

{{{
rss: .....
imdb_lookup: yes
tvdb_lookup: yes
regex:
  accept:
      - Game Of Thrones
quality:
  upgrade: true
  accept:
    - 720p hdtv
    - 1080p webdl
}}}
 
Identifers set by meta plugins

- Identifer(name='tvdb_id', value='123456')
- Identifer(name='imdb_id', value='123456')
- Identifer(name='series_id', value='S01E01', required=True) ... TODO: required?

First run (Game.Of.Thrones.S01E01.HDTV)
- Regex accepts
- Check if desired quality downloaded, NO (not desired quality) -> leave alone

Second run (Game.Of.Thrones.S01E01.720p)
- Regex accepts
- Check if desired quality downloaded, NO -> leave alone

Third run (Game.Of.Thrones.S01E01.720p)
- Regex accepts
- Check if desired quality downloaded, YES -> reject

Third run (Game.Of.Thrones.S01E01.1080p)
- Regex accepts
- Check if desired quality downloaded, NO -> leave alone

