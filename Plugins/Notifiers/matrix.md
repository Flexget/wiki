---
title: Matrix
description: 
published: true
date: 2022-12-07T07:19:17.024Z
tags: 
editor: markdown
dateCreated: 2022-12-07T04:46:20.436Z
---

# [Notifiers](/Plugins/Notifiers) > Matrix
> Join is a part of the [notifier](/Plugins/Notifiers) plugin system.
{.is-success}

# Overview
Sends messages via Matrix protocol.  Uses a simple **Access Token** authentication to send messages to a **room**.  Using an Access Token allows for encrypted messages to be used, unlike bots which only work on unencrypted rooms.

## Config
All fields are required.

| Options | Description | 
| --- | --- |
| server | Matrix hostname to integrate to (required) |
| token | Is available in Element under Help/About. (required) |
| room_id | Is available in Element under room settings. (required) |

## Example

```yaml
notify:
  entries:
    via:
      - matrix:
          server: "https://matrix.org"
          token: senders token
          room_id: room identifier
```

# Element Steps

## Room ID

Find or Create a matrix room.  Right-click the room icon and select Settings.  Click the menu item "Advanced" and find the heading "Room Information".  You should have a Internal Room ID key which looks like: 
`!uyR5dGzDkPOLIODSzy:matrix.org`

## User Token
This is your account key that allows for sending and receiving messages from your matrix account.  This is a private key and you should only paste it in secure locations.

Right click your account Icon and select "All Settings".  Navigate to "Help & About".  Select the heading "Advanced" and open the draw for Access Token.  It should look like:
`yus_THSKS60aWHjdPsvjspvekniadni_4i89TH`

**Your access token gives full access to your account. Do not share it with anyone.**  Please treat it like your other passwords used flexget config.