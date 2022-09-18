---
title: regexp
description: 
published: true
date: 2022-09-18T05:15:37.009Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:10:35.699Z
---

## Regexp
Use regular expression to Accept or Reject entries. FlexGet uses python regexp format and all matching is done case insensitive. This plugin may look a bit scary but in reality you rarely want anything more than what simple examples describe.

**Note:** If you are having trouble figuring out how to create your desired regexp, [RegExr](http://www.gskinner.com/RegExr/) is a very helpful tool. You can also try [--try-regexp](/Plugins/try_regexp) interactively.

### Simple examples
Accept entries matching regexp(s).

```
regexp:
  accept:
    - regexp 1
    - regexp 2
```

Reject permanently entries matching regexp(s). This should be used when you absolutely do not want to download matching entries, even if some other plugin (ie. `imdb`, `series`) would deem them acceptable.

```
regexp:
  reject:
    - regexp 1
    - regexp 2
```

### Examples
Require something to be in the title by rejecting everything that does **not** have it.

```
regexp:
  reject_excluding:
    - regexp
```

This can be combined with some other accepting filter.

Multiple operations. This would be useful when grabbing some shows and they appear with unwanted languages as well.

```
regexp:
  accept:
    - show name
  reject:
    - german
    - sweden
```

## Set custom path
Any regexp rule can set custom path for matching entry.

### Example
```
regexp:
  accept: 
    - regexp here: ~/custom/path
```

or

```
regexp:
  accept: 
    - regexp here:
        path: ~/custom/path
```

## Search Custom Fields
By default, regexp plugin will only try to match in the title and description fields of the entry. If you would like to specify custom fields to search in, you can do so either per regexp, or for the whole plugin at once. You can either list a single field to search from, or a list of fields.

### Examples
Reject drama from the tvdb_genre field which is filled by [thetvdb_lookup](/Plugins/thetvdb_lookup) plugin.
```
regexp:
  reject:
    - drama:
        from: tvdb_genres
```
Make sure all regexps only apply to title field.
```
regexp:
  accept:
    - good.stuff
  reject:
    - bad.things
  from: title
```

## Full syntax
```
regexp:
  <operation>:
    - pattern 1
    - pattern 2: <custom path>
    - pattern 3:
        [not]:
          - pattern 4
        [path]: <custom path>
        [from]: <entry field> # applies to this pattern
        [set]:
            <entry field>: <value>
  [rest]: <operation>
  [from]: <entry field> # applies to all patterns
```

^[] = optional, <> = value^

Available operations: `accept`, `reject`, `accept_excluding` and `reject_excluding`.
Configuration may contain any number and combination of different operations.

## Operations described
### accept
If any of the regexps from the list match, accept the entry.

### reject
If any of the regexps from the list match, reject the entry.

### accept_excluding
If any of the regexps from the list do not match, accept the entry.

### reject_excluding
If any of the regexps from the list do not match, reject the entry.