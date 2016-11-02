## Identified by
Specify how episode number is detected.

**Example:**

```
series:
  - pioneer one:
      identified_by: ep
```

Possible values: `ep`, `sequence`, `date`, `id`, `auto`

Default value is `auto` which uses episode history to detect what to use. In absence of reliable history all formats are accepted.

### What is "ep"
Series which are identified by season, episode. 

**Examples:**

 * S01E02
 * 01x02

### What is "sequence"
Any series that are numbered in increasing order.

**Examples:**

 * 01
 * 23
 * 157

### What is "date"
Series that are identified by air date.

**Examples:**

 * 01-01-2012
 * 2012.2.6
 * 04-13-11

**Note:** If a date is ambiguous, due to different date formats used in different countries, the most recent interpretation is used (that isn't in the future.) You can use the `date_yearfirst` and `date_dayfirst` options to alter this behavior.

```
identified_by: date
date_yearfirst: yes
```

### What is "id"
Series that are identified by anything unique. There are not many built in regexps for this mode, it is mostly useful when your series do not fit into another mode, and you define your own `id_regexps`

**Examples:**

 * cat
 * foobar

Since id is free format, it doesn't support [tracking](/Plugins/series/tracking).

### Custom matching
FlexGet identifies almost everything by default, but sometimes it may be necessary to customize matching. This can be achieved via [ep_regexp and id_regexp](/Plugins/series/regexps).