= Quality =

Allows specifying acceptable qualities. All other qualities will be rejected.

''' Example: '''

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