= Quality =

Allows specifying acceptable qualities. All other qualities will be rejected. (NOTE: If you are using another plugin with it's own quality detection, i.e. [wiki:series series], it might offer more functionality. Also mixing series quality options and quality plugin will cause weird behaviour.)

== Simple Usage ==

With the simple usage, you just specify which quality you want.

{{{
quality: 720p+ hdtv
}}}

Any valid [wiki:Plugins/quality#Requirements quality requirements] string can be used here.

You can also use a list form to specify multiple quality requirement strings that are acceptable.

{{{
quality:
  720p hdtv
  1080p webdl
}}}

[[Include(wiki:Qualities)]]