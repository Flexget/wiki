---
title: decompress
description: 
published: true
date: 2025-08-14T03:49:35.158Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:03:26.935Z
---

# Decompress

This plugin requires the rarfile Python module and unrar command line utility to extract RAR archives. To install the Python module run:

```cmd
pip install flexget[rarfile]
```

Extracts files from Zip or RAR archives. By default this plugin will extract to the same directory as the source archive, preserving directory structure from the archive.

The unrar utility can be installed using your package manager of choice (e.g. apt, macports) or can be downloaded directly from [RARLab](http://www.rarlab.com/rar_add.htm).

## Options

| **Name** | **Info** | **Description** |
| --- | --- | --- |
|  to  |  Text  |  Destination path; supports Jinja2 templating on the input entry. Fields such as series_name must be populated prior to input into this plugin using metainfo_series or similar. If no path is specified, archive contents will  be extraced in the same directory as the archve itself.  |
|  keep_dirs  |  Yes\|No |    Indicates whether to preserve the directory  structure from within the archive in the destination path.  Defaults to `yes` |
|  mask  |  Text  |  Shell-style file mask; any matching files will be extracted. When used, this field will override regexp.  |
|  regexp  |  Text  |  Regular expression pattern; any matching files will be extracted. Overridden by mask if specified.  |
|  unrar_tool  |  Text  |  Specifies the path of the unrar tool. Only necessary if its location is not defined in the operating system's PATH environment variable.  |
| delete_archive |Yes\|No|  Delete this archive after extraction is completed. Defaults to `No`||

**Examples**

If simply you want to decompress to the same directory as the archive without any filtering, the plugin can be enabled with a simple boolean:

```yaml
decompress: yes
```

Here's a more complicated example:

```yaml
decompress:
  to: '/Volumes/External/TV/{{series_name}}/Season \{{series_season}}/'
  keep_dirs: yes
  regexp: '\.mkv'
```

And in the context of a complete task:

```yaml
move-series-rar:
  accept_all: yes
  parsing:
    series: guessit
  metainfo_series: yes
  require_field:
    - series_name
    - series_season
  filesystem:
    path: /Volumes/Drobo/downloads/
    recursive: yes
    regexp: '\.(rar|r0+[01]|zip)'
  decompress:
    to: '/Volumes/Drobo/TV/{{series_name}}/Season \{{series_season}}/'
    keep_dirs: no
    delete_archive: yes
```