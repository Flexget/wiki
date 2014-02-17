= Assume Special =

If True, causes any entries with no series numbering detected to be treated as a special and processed accordingly.

Example:
{{{
series:
  - the show:
      assume_special: True
}}}

This would cause an entry called 'The Show S1 SOMETHING' to be accepted as a special.

'''Warning: Will result in FlexGet accepting season packs and lots of stuff which would normally be rejected. Use with caution.'''