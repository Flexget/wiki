= Preset =

Allows defining presets configs for plugins and re-using them in multiple tasks. Note that presets are not executed separately. All included presets will be merged into the task before it is run.

{{{
presets:

  tv:
    series:
      - foo
      - bar
    download: ~/download/series/

  movies:
    imdb:
      min_score: 6.2
      min_votes: 5000
    download: ~/download/movies/

tasks:
  some_task:
    rss: http://example.com
    preset: tv

  another_task:
    rss: http://example2.com
    preset: movies

  third_task:
    rss: http://example3.com
    preset: 
      - tv
      - movies

}}}

== Execute tasks with a given preset ==

To execute all tasks that have certain preset you can use `--preset NAME`

'''Examples:'''

{{{
--preset movies
}}}

{{{
--preset tv
}}}

== Merging limitations ==

In case you're using multiple presets in a task and more than one preset has same plugin, they must be
configured in same format for merge to be possible.

'''Incompatible:'''

{{{
preset-a:
  series:
    - foo
    - bar

preset-b:
  series:
    settings:
      720p:
        timeframe: 12 hours
    720p:
      - xxx
      - yyy
}}}

Why is it incompatible?

''Preset-a'' has list under series where as ''preset-b'' has key value-pairs.

For merging to work they need to be in same format:

'''Compatible:'''

{{{
preset-a:
  series:
    normal:
      - foo
      - bar

preset-b:
  series:
    settings:
      720p:
        timeframe: 12 hours
    720p:
      - xxx
      - yyy
}}}

In which case the result is:

{{{
series:
  settings:
    720p:
      timeframe: 12 hours
  720p:
    - xxx
    - yyy
  normal:
    - foo
    - bar
}}}

Simple values cannot never be merged. So for example multiple `rss: <url>` or `include: <file>` cannot be defined within task & preset. Include accepts list format for files so that can be used instead. 

== Global preset ==

Allow specifying plugins for every task without being explicitly told so. Avoid using this since it WILL shoot you in the feet at some point if you're not careful.

{{{
presets:
  global:
    download: ~/torrents/
tasks:
  task-a:
    rss: ...
  task-b:
    rss: ...
}}}

Both tasks task-a and task-b use automatically global preset.

The global preset can be disabled on a specific task by including the special preset {{{no_global}}} i.e.

{{{
preset: no_global
}}}

or, if you also need to include other presets

{{{
preset:
  - no_global
  - preset_b
}}}
