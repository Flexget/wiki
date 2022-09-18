---
title: filesystem
description: 
published: true
date: 2022-09-18T05:05:08.704Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:05:06.058Z
---

# Filesystem
Uses local path content as an input. Generate entries from files, dirs & symlinks found in path(s).   


|  Option  |  Description  |
| --- | --- |
| **path** | One or more paths. Must be unique. Mandatory when using an object in config. |
| **mask** | File mask, like '*.mkv'   |
| **regexp** | Regexp like <code>.*\.(avi&#124;mkv)$</code>. Note: If both `mask` and `regexp` are present, `mask` will be used.  |
| **recursive** | Recursion flag. Can be set to `True`, `False` or an integer. `True` will recurse without limit, `False` will not recurse and the integer value will decide how deep the recursion should go. Minimum value is 2 levels deeps, (1 levels is similar to no recursion). Default is `False` |
| **retrieve** | Decided which type of objects should be made into entries. Accepts one or more of the following: `files`, `dirs` `symlinks`. Default is all of them.   |

It isn't necessary to send an object including parameters, there are many acceptable permutations. See examples below:

Entries will have following fields:


| Name | Value |
| --- | --- |
| url | Location in URI form (file://...) |
| location | Location in raw form (/foo/bar) |
| title | File or Directory name |
| accessed | Datetime |
| modified | Datetime |
| created | Datetime |
    
## Examples
### Single path

```yaml
filesystem: /storage/movies/
```
    
### List of paths
```yaml
filesystem:
  - /storage/movies/
  - /storage/tv/
```

### Object with list of paths
```yaml
filesystem:
  path:
    - /storage/movies/
    - /storage/tv/
  mask: '*.mkv'
```

### Using Recursion
```yaml
filesystem:
  path:
    - /storage/movies/
    - /storage/tv/
  recursive: 4  # 4 levels deep from each base folder
  retrieve: files  # Only files will be retrieved
```

### Extended Recursion
```yaml
filesystem:
  path:
    - /storage/movies/
    - /storage/tv/
  recursive: yes  # No limit to depth, all sub dirs will be accessed
  retrieve:  # Only files and dirs will be retrieved
    - files
    - dirs
  regexp: '.*\.(avi|mkv|mp4|m4v|iso)$'
```