= Allow_backfill =

If you already have part of a show, and want to allow !FlexGet to retrieve episodes from the past, without [wiki:Plugins/series/advancement episode advancement] rules rejecting them, you can use the `allow_backfill` setting.

== Valid Values ==
The only allowed values for this setting are `yes` and `no`

=== Setting from config ===

You can set the allow_backfill value directly from the config.

{{{
series:
  - pioneer one:
      allow_backfill: yes
}}}