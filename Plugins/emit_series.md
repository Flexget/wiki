= Emit Series Input =

Creates an [wiki:Entry Entry] for the next episode needed in each series you have configured in the [wiki:Plugins/series series] plugin (intended to be used with the [wiki:Plugins/discover discover] plugin). You must have either [wiki:Plugins/series series] or [wiki:Plugins/configure_series configure_series] plugin configured in the same task for this to work. 

If !FlexGet has not seen the series for some time and locked to specific episode numbering scheme the [wiki:Plugins/series/begin begin] setting for the show should be used or emit_series can not guess what to emit.

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

If you would like to start emitting every show automatically without setting the begin episode, you can configure emit_series like this:
{{{
emit_series:
  from_start: yes
}}}

Additionally, if you want flexget to attempt to retrieve any episodes you're missing from any season, you can configure emit_series like this:
{{{
emit_series:
  backfill: yes
}}}

Note that with this setting, you must also set the allow_backfill option on each series you want to allow_backfill in the [wiki:Plugins/series series] plugin