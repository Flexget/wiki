= Reject Failed =
This plugin rejects entries that have failed more than three times (by default) in the past. This will allow any potential replacements to be accepted instead of the same failing entry.

This plugin is a [wiki:Builtin builtin] and does not need to be explicitly placed in your feed unless you would like to override the default number of failures needed before rejection. Number of needed failures can be configured like:
{{{
reject_failed: <# of failures>
}}}
