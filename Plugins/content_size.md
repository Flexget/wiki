= Content size =

Allow specifying minimum and maximum sizes for contents such as torrents and nzbs. By default the plugin operates in "strict" mode where if the size of a download cannot be determined it will be rejected.

=== Example: ===

{{{
content_size:
  min: 12
  max: 1200
  strict: false
}}}

Size is given in MB

This would reject all torrents below 12MB and above 1200MB and over rides the strict behaviour. Same would work also for nzbs.
