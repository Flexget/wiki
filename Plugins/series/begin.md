= Begin =

If you already have part of a show, and need to specify where !FlexGet should begin downloading, it can be done using the `begin` option. This should be equal to the first episode you want !FlexGet to accept. This may not be needed in the general case, since !FlexGet will not skip forward and back seasons due to [wiki:Plugins/series/advancement episode advancement] functionality. If you are using [wiki:Plugins/emit_series emit_series] it is important to set this so that emit_series knows which episode to start searching from. There are two ways to set this option, from the config, or from the CLI.

== Valid Values ==
The begin option can be set on series that are use 'ep', 'sequence', or 'date' `identified_by` mode. Setting the `begin` option will also set `identified_by` for the series, based on the format of the episode identifier used. Format for episode identifiers is as follows:

'''ep:''' SXXEYY, e.g. `S03E04`

'''sequence:''' Just the episode number, e.g. `13`

'''date:''' YYYY-MM-DD, e.g. `2013-03-04`

=== Setting from CLI ===

To set begin for a show from the CLI, use the `series begin` command. e.g.
{{{
flexget series begin "name of series" S02E01
}}}


=== Setting from config ===

You can also set the begin value directly from the config.

{{{
series:
  - pioneer one:
      begin: S02E01
}}}