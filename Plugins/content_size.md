= Content size =

Allow specifying minimum and maximum sizes for contents such as torrents and nzbs.

=== Example: ===

{{{
content_size:
  min: 12
  max: 1200
}}}

Size is given in MB

This would reject all torrents below 12MB and above 1200MB. Same would work also for nzbs.
