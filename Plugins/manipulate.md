---
title: manipulate
description: 
published: true
date: 2023-07-15T16:59:41.080Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:54.028Z
---

# Manipulate
Mainly for advanced users only. Allows setting and cleaning entry fields with regexp.

Syntax:

```
manipulate:
  - <destination field>:
      [phase]: <phase>
      [from]: <source field>
      [separator]: <value>
      [extract]: <regexp>
      [replace]:
        regexp: <regexp>
        format: <regexp>
      [remove]: <boolean>
```

Valid values for phase are: metainfo and filter, metainfo is the default behavior.

To see what results your configuration has, use [--dump](/Plugins/--dump) plugin to display all entries after execution.

When using extract functionality manipulate will join all returned groups together with separator. The default separator is single space.

### Example 1
Title is filled with garbage that series plugin does not like.

eg.

```
[48952] The Series S01E01 720p
```

This could be fixed by removing the [48952]

```
manipulate:
  - title:
      extract: \[\d+\](.*)
```

The (.*) part is what this regexp is extracting (capture group), so everything after those numbers.

Regexp can return any number of groups, value is combination of these (separated with a space).

### Example 2
Some badly written site has invalid URLs. Uses \&amp; instead of &

```
manipulate:
  - url:
      replace:
        regexp: '&amp;'
        format: '&'
```

Currently these are fixed automatically by [urlfix](/Plugins/urlfix) plugin.

### Example 3
You can do multiple manipulates in a row, and they will be executed in order. You can also do multiple manipulates on the same field.

```
manipulate:
  - title:
      extract: .*\[\s*(.*)\s*\]-.*
  - filename:
      from: title
  - title:
      replace:            
        regexp: '[\.-]'
        format: ' '
```

### Example 4
You can control how the regex hits are output using \1, \2, etc in format.

```
manipulate:
  - title:
      replace:            
        regexp: '(.*)/(.*)/(.*)'
        format: '\2.\1.\3'
```

### Example 5
The series plugin operates on both the title and description fields. If you want to exclude the description field, you can simply remove it:

```
manipulate:
  - description:
      remove: yes
```
