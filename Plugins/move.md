= Move =

''TODO: Improve documentation''

Syntax:

{{{
move:
  [path]: move accepted entries to, allows value replacement
  [unpack_safety]: enable or disable unpacking safety checks, enabled by default. causes 1 sec delay per processed entry
  [clean_source]: delete source directory if it has less MB left than given after move
}}}

[] = optional

Entry field "to" can be used to override given path.