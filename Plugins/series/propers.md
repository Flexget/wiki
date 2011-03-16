== Propers ==

Default behavior is to download propers always.

To disable propers completely:

{{{
series:
  - some series:
      quality: 720p
      propers: no
}}}

To specify timeframe in which propers are accepted:

{{{
series:
  - some series:
      quality: 720p
      propers: 12 hours
}}}

Accepted format: NUM (minutes|hours|days|weeks)
