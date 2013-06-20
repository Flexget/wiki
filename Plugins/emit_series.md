= Emit Series Input =

Creates an [wiki:Entry Entry] for the next episode needed in each series you have configured in the [wiki:Plugins/series series] plugin (intended to be used with the [wiki:Plugins/discover discover] plugin). You must have either [wiki:Plugins/series series] or [wiki:Plugins/import_series import_series] plugin configured in the same task for this to work. If !FlexGet has never seen an episode of a given show, it must have the [wiki:Plugins/series/begin begin] setting set for the show so it knows the first episode to output.

=== Example ===

{{{
discover:
  what:
  - emit_series: yes
  from:
  - torrentz: verified
series:
  - my show:
      begin: S01E01
  - other show:
      begin: S03E01
}}}