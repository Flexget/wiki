= Input !AppleTrailers =

Adds support for [http://trailers.apple.com/ Apple Trailers] as an input source.

== Example: ==

{{{
apple_trailers: 480p
accept_all: yes
headers:
  user-agent: "QuickTime/7.6.2"
download: ~/movies/trailers
}}}

This would download all trailers with 480p resolution. Resolution is a choice of: ipod, '320', '480', 640w, 480p, 720p, 1080p.

The User-Agent header needs to be set. Apple does U-A sniffing for direct downloads as of 2011-11-8 (maybe earlier).