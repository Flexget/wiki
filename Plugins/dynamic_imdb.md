= Dynamic IMDB =
This plugin creates an [wiki:Entry entires] based on an IMDB person, company or character. Additional filters like content types and job types can be added to the config to limit down the generated list.
The main purpose of this plugin is to be used with the [wiki:movie_queue movie_queue] plugin as an input, but it can be also used with [wiki:Plugins/configure_series configure_series] if content is set to TV.
This plugin is based on [http://imdbpy.sourceforge.net/ IMDBPY] and it is required {{{ pip install imdbpy }}}

== Plugin Settings ==

The only required setting is ID. The plugin can be used in several formats.
For example:
{{{
    dynamic_imdb: ch0001354
}}}
Or:
{{{
    dynamic_imdb: 
      id: ch0001354
}}}
More than one can be used:
{{{
    dynamic_imdb:
      id:
        - nm0004874 # Vin Diesel
        - nm0000246 # Bruce Willis
        - nm0000195 # Bill Murray 
        - nm0565250 # Melissa McCarthy
        - nm0005458 # Jason Statham
        - nm0000093 # Brad Pitt
        - nm0001125 # Benicio Del Toro
}}}
These two examples are equal. The only important part is to give the full IMDB ID in any form. Note that only person (`nm` prefix), company (`co` prefix) and character (`ch` prefix) are supported.
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''id'''||As listed above, one or more strings that contains one of the prelisted accepted IMDB IDs. At least one is Required.||
||'''job_types'''||A string or list with one or more of the following: `actor`, `director`, `producer`, `writer`, `self`, `editor`, `miscellaneous`, `editorial department`, `cinematographer`, `visual effects`, `thanks`, `music department`, `in development`, `archive footage` and `soundtrack`. Default is `actor`. Relevant only when filtering for `person`. ||
||'''content_types'''||A string or list with one or more of the following: `movie`, `tv series`, `tv mini series`, `video game`, `video movie`, `tv movie`, `episode`. Default is `movie`||
||'''max_entries'''|| The maximum number of entries that can return. This value's purpose is basically flood protection against unruly configurations that will return too many results. Default is `200`. ||
}}}
=== Example: ===
{{{
   dynamic_movie_queue:
     dynamic_imdb:
       id: nm0005212
       job_types:
         - actor
         - director
       content_types: tv series
       accept_all: yes
       movie_queue: add
}}}