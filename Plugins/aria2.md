---
title: aria2
description: 
published: true
date: 2022-12-03T03:38:20.209Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:02:21.992Z
---

# Aria2
>**Requirements:** Aria2 running and in daemon mode, with XML-RPC enabled 
{.is-info}

Passes URIs in entries to the [Aria2 downloader](http://aria2.sourceforge.net). Supports HTTP, HTTPS, FTP, Torrent, Magnet.

Start can be simple as

```cmd
aria2c --enable-rpc --rpc-listen-all
```

Which is also very insecure. See Aria2 documentation for improving on that.

### Options

| Name | Default | Required | Description |
| --- | --- | --- | --- |
| server | localhost | No | Hostname or IP of the server where Aria2 is running and has XML-RPC enabled. |
| port | 6800 | No | Port to connect to on the server listed above. |
| username | N/A | No | Username used to connect to the aria2 XML-RPC server. (Corresponds to ```rpc-user``` in the Aria2 config file.) |
| password | N/A | No | Password used to connect to the aria2 XML-RPC server. (Corresponds to ```rpc-passwd``` in the Aria2 config file.)|
| path | N/A | Yes | Output directory|
| secret | N/A | No | Aria2 `rpc-secret`|
| options | N/A | No | Any Aria2 options in key-value format.|

### Example

```yaml
aria2:
  path: ~/downloads/
```