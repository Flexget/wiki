---
title: ftp_list
description: 
published: true
date: 2022-09-18T05:06:06.157Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:06:03.487Z
---


## FTP List

Generate entries from a remote FTP server. Entries can be downloaded via [ftp_download](/Plugins/ftp_download) plugin or by passing it to other output plugins. See examples for details.

**Note**: This plugin requires a 3rd party called [ftputil](http://ftputil.sschwarzer.net/trac/wiki/WikiStart). `pip install ftputil` in order to use.

### Plugin Settings

Currently the following settings are required:


|  Option  |  Type  |  Description  |
| --- | --- | --- |
| **username** | text | Username to use  |
| **host** | text | Host to connect to. Example `host.domain.com`  |

The following settings are optional:


|  Option  |  Type  |  Description  |
| --- | --- | --- |
| **password** | text | Password.  |
| **port** | integer |  Connection port. Default is 21  |
| **use_ssl** | boolean |  Wether or not use SSL connection. Default is no  |
| **dirs** | text or list |  Choose which dirs to iterate over. Must be relative to base dir. Default is basedir.  |
| **retrieve** | text or list | Type of objects to retrieve. Can be `files`, `dirs` and `symlinks`. Set to `files` by default. |
| **recursion** | boolean |  Choose if to recursively retrieve object from selected dirs. Default is false  |
| **recursion_depth** | boolean |  Relative level to retrieve, relevant only if `recursion` is true, set to infinity by default.  |

#### Examples:

This is a complete task

```yaml
taskname:
  ftp_list:
    username: username
    password: password
    host: host.domain.com
    port: 27015
    use_ssl: yes
    dirs: 
      - A.Dir.Name
      - AnotherDir
    retrieve: 
      - dirs
      - files
    recursion: yes
    recursion_depth: 2 
  accept_all: yes
  ftp_download: 
    ftp_tmp_path: /flexget_test

```