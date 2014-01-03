= Template =

Allows defining config templates containing one or more plugins and re-using them in multiple tasks. Note that templates are not executed separately. All included templates will be merged into the task before it is run.

{{{
templates:

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
    template: tv

  another_task:
    rss: http://example2.com
    template: movies

  third_task:
    rss: http://example3.com
    template: 
      - tv
      - movies

}}}

== Execute tasks with a given template ==

To execute all tasks that have certain template you can use `--template NAME`

'''Examples:'''

{{{
--template movies
}}}

{{{
--template tv
}}}

== Merging limitations ==

In case you're using multiple templates in a task and more than one template has same plugin, they must be
configured in same format for merge to be possible. Additionally (as of 1.2), all plugins, whether configured in a task or a preset, must be valid on their own, before merging. This means that all required fields must be included anywhere a plugin is configured, rather than having multiple presets merged to create a complete one.

'''Incompatible:'''

{{{
template-a:
  series:
    - foo
    - bar

template-b:
  series:
    settings:
      720p:
        timeframe: 12 hours
    720p:
      - xxx
      - yyy
}}}

Why is it incompatible?

''Template-a'' has list under series where as ''template-b'' has key value-pairs.

For merging to work they need to be in same format:

'''Compatible:'''

{{{
template-a:
  series:
    normal:
      - foo
      - bar

template-b:
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

Simple values cannot never be merged. So for example multiple `rss: <url>` or `include: <file>` cannot be defined within task & template. Include accepts list format for files so that can be used instead. 

== Global template ==

Allow specifying plugins for every task without being explicitly told so. Avoid using this since it WILL shoot you in the feet at some point if you're not careful.

{{{
templates:
  global:
    download: ~/torrents/
tasks:
  task-a:
    rss: ...
  task-b:
    rss: ...
}}}

Both tasks task-a and task-b use automatically global template.

The global template can be disabled on a specific task by including the special template {{{no_global}}} i.e.

{{{
template: no_global
}}}

or, if you also need to include other templates

{{{
template:
  - no_global
  - template_b
}}}
