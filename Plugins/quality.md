= Quality =

Allows specifying acceptable qualities. All other qualities will be rejected. (NOTE: If you are using another plugin with it's own quality detection, i.e. series, you should use it's built in quality system)

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

== Min/Max Support ==

If you would like to specify a range of qualities, you can use this form:

{{{
quality:
  min: hdtv
  max: 1080p
}}}

This will reject all qualities worse than hdtv, and better than 1080p. It is not required to specify both min and max, you can specify an open ended range using just one of them.

== Known Qualities ==

The following qualities are known, and listed in decending order of quality. The second column contains alternate formats that are recognized.
 ||'''Name'''||'''Alternate Forms'''||
 ||1080p||1080, 1920x1080||
 ||1080i||
 ||web-dl||
 ||720p||720, 1280x720||
 ||720i||
 ||hr||
 ||bdrip||
 ||dvdrip||dvd||
 ||480p||480||
 ||hdtv||
 ||bdscr||
 ||dvdscr||
 ||sdtv||pdtv||
 ||dsr||dsrip||
 ||!r5||
 ||tc||
 ||preair||
 ||cam||
 ||workprint||