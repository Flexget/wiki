= Prefer Specials =

If True, cause entries matching both a normal ID type (ep, sequence, etc) and special to be flagged as specials. If False, entry will be flagged as the normal ID type. Defaults to False.

Example:
{{{
series:
  - My Series:
      prefer_specials: True
}}}

|| '''Title''' || '''prefer_specials:''' || '''Resulting series_id_type:''' ||
|| the show s03e04 special || True || special ||
|| the show s03e04 special || False || ep ||