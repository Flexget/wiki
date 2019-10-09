## Advanced matching with regexps
The standard name matching works quite well, but in some cases you may need to specify regexp(s) manually. Usually the `name_regexp` when series is written in multiple different ways.

**Notes:**
 
 * **Use these only if you're having problems with matching**. Built in logic should be able to handle 99% of cases without any need for manual regexp tweaking.
   * If you have titles with confusing crap in them, use [manipulate](/Plugins/manipulate) plugin to clean them!
 * `name_regexp` is useful for series which are written in more than one way
 * If specifying name_regexp(s) make sure that these match **only to the given series NAME.**
 * If specifying ep_regexp or id_regexp you will most likely want to lock that series into that format with [identified_by](/Plugins/series/identified_by) option.
 * Pay attention to the *indentation* here

**Example:**

```
series:
  - some series:
      ep_regexp: (\d\d)-(\d\d\d)     # must return TWO groups, both being numeric values
  - another series:
      id_regexp: (\d\d\d)            # can return any number of groups
  - third series
```

All above regexps also accept multiple regular expressions in list form.

## Name regexp
For example if `some series` appears in multiple different naming conventions, you can give list of regexps that match to series name. The match is tried from title AND description fields.

```
- some series:
    name_regexp:
      - ^some.series
      - ^some.srs
      - ^some.series.2011
```

### Episode numbering matching
ep_regexp is for series enumerated by season and episode numbers (eg, S04E01). Naive example:

```
ep_regexp:
  - s(\d+)e(\d+)
  - s(\d+)ep(\d+)
```

id_regexp is for series that are not enumerated by season/episode numbering. Naive example:

```
id_regexp:
  - (\d\d\d\d).(\d+).(\d+)
  - (\d+).(\d+).(\d\d\d\d)
```

`date_regexp` and `sequence_regexp` can also be defined for series [identified by](/Plugins/series/identified_by) those respective numbering schemes.

User defined regexps takes priority over the built-in expressions, but do not disable them.

Specifying `ep_regexp` disables all `id_regexp`'s and vice versa.