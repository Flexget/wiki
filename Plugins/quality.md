= Quality =

Allows specifying acceptable qualities. All other qualities will be rejected. (NOTE: If you are using another plugin with it's own quality detection, i.e. series, it might offer more functionality. Also mixing series quality options and quality plugin will cause weird behaviour.)

== Simple Usage ==

With the simple usage, you just specify which quality you want.

{{{
quality: 1080p
}}}

This would reject all entries that are not 1080p.

If you want to specify multiple acceptable qualities it can be done like this:

{{{
quality:
  - 720p
  - 1080p
}}}

== !Min/Max Support ==

If you would like to specify a range of qualities, you can use this form:

{{{
quality:
  min: hdtv
  max: 1080p
}}}

This will reject all qualities worse than hdtv, and better than 1080p. It is not required to specify both min and max, you can specify an open ended range using just one of them.

[[Include(wiki:Qualities)]]