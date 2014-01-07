= Assume Quality =

Applies [wiki:Qualities quality components] to [wiki:Entry entries] that match specified quality requirements.
When a quality is applied, any components which are unknown in the entry are filled from the applied quality. Quality requirements are tested in order of decreasing precision (the number of components matched, i.e. "720p h264" is more precise than "1080p" so gets tested first), and applied as matches are found. A pseudo-requirement "any" is also supported, which will match all qualities and be tested last. Using the simple configuration is the same as specifying an "any" rule.

== Examples ==
=== Simple configuration ===

{{{#!yaml
assume_quality: 1080p webdl 10bit truehd
}}}

This will set the resolution of any entries without a resolution to '1080p', the source of any entries without a source to 'webdl', and so on.

=== Advanced configuration ===
{{{#!yaml
assume_quality:
  hdtv: 720p
  720p hdtv: 10bit
  '!ac3 !mp3': bluray
  any: 720p h264
}}}

||An entry matching...  ||Will be set to||
||hdtv                  ||720p     ||
||720p and hdtv         ||10bit    ||
||Neither ac3 nor mp3   ||bluray   ||
||any                   ||720p h264||