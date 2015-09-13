= Smart IMDB =
This plugin creates an [wiki:Entry entires] based on an IMDB person, company or character. Additional filters like content type, job types, years and etc can be added to the config to limit down the generated list.
The main purpose of this plugin is to be used with the [wiki:movie_queue movie_queue] plugin as an input, but it can be also used with [wiki:Plugins/configure_series configure_series] if content is set to TV.
This plugin is based on [http://imdbpy.sourceforge.net/ IMDBPY] and it is required {{{ pip install imdbpy }}}

== Plugin Settings ==

The only required setting is ID. The plugin can be used in several formats.
For example:
{{{
    smart_imdb: 'http://www.imdb.com/character/ch0001354/?ref_=tt_cl_t1'
}}}
Or:
{{{
    smart_imdb: 
      id: ch0001354
}}}
These two examples are equal. The only important part is to give the full IMDB ID in any form. Note that only person (`nm` prefix), company (`co` prefix) and character (`ch` prefix) are supported.
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''id'''||As listed above, any string that contains one of the prelisted accepted IMDB IDs. Required.||
||'''job_types'''||A string or list with one of the following: `actor`, `director`, `producer`, `writer`, `self`, `editor`, `miscellaneous`, `editorial department`, `cinematographer`, `visual effects`, `thanks`, `music department`. Default is `actor`. Relevant only when filtering for `person`. ||
||'''content_types'''||A string or list with one of the following: `movie`, `tv series`, `tv mini series`, `video game`, `video movie`, `tv movie`, `episode`. Default is `movie`||
||'''include_genres'''||A string, list or object that defined which genres must be part of the filtered item. Contains `genres` and `match_type` property. If using an object, `genres` is mandatory.||
||'''exclude_genres'''|| A string, list or object that defined which genres must '''NOT''' be part of the filtered item. Contains `genres` and `match_type` property. If using an object, `genres` is mandatory. ||
||'''match_type'''||Relevant under `include_genres` or `exclude_genres`. Defined the matching type of the requested genres. Can be `any`, `all` or `exact`. Any will pass the test if any of the listed genres are a part of the filtered item.`all` tries to match all of the requested gernes and `exact` will pass only if all of the requrested genres and no more are part of the item. Default is `any`. See config for usage. ||
||'''rating'''|| A number between 0 and 10 that filters the corresponding rating that an item must have in order to pass the filter. ||
||'''votes'''|| A number higher than 0 that filters the corresponding number votes that an item must have in order to pass the filter. ||
||'''years'''|| A string that filters the item based on its release year. Can be 1 of four formats: `year`, `year-`, `-year` and `year-year`. See config for details. ||
||'''actor_position'''|| A number great than 0 that specifies the minimum position that an actor must be listed in case in order to pass filter. Releavnt only when filtering for `person` and job_types include `actor`. ||
||'''strict_mode'''|| A boolean value that determines what to do in case an item does not have year, rating or votes listed and the configuration holds any of those. If set to 'True', it will cause an item that does not hold one of these properties to fail the filter. Default is 'False'. ||
||'''max_entries'''|| The maximum number of entries that can return. This value's purpose is basically flood protection against unruly configurations that will return too many results. Default is 200. ||
}}}
=== Example: Get all Marvels Studios movies, from 2008, with rating higher than 6, genres must include action and comedy, and no short films. Add to movie_queue ===
{{{
    smart:
      smart_imdb:
        id: 'co0051941'
        years: '2008-'
        rating: 6
        include_genres:
          genres:
            - action
            - comedy
          match_type: all
        exclude_genres: short
      accept_all: yes
      movie_queue: add     
}}}

=== Example: Get all Steven spielbergs movies as a director, from 2009-2015, rating 7, votes 10000, genres should include war . Add to movie_queue ===
{{{
    smart:
      smart_imdb:
        id: 'http://www.imdb.com/name/nm0000229/?ref_=nv_sr_1'
        job_types: director
        years: '2009-2015'
        rating: 7
        votes: 10000
        include_genres: war
      accept_all: yes
      movie_queue: add
}}}

