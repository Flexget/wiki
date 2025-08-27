---
title: Chat
description: 
published: true
date: 2025-08-27T13:34:48.211Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:48:47.761Z
---

# Chat
Chat can be accessed via multiple ways. We are using a bot to sync chat between all of the chat services.

## Rich Web Clients
There are several rich web interfaces we support, accessible anywhere, with backlog built in. If you are not already using IRC for anything else, these are probably the nicest chatting methods.

- Matrix protocol:
  - [Matrix](https://matrix.to/#/#flexget:matrix.org) (Matrix official server)
  - [Gitter](http://gitter.im/Flexget/Flexget) (Gitter is another Matrix server)
- [Slack](https://join.slack.com/t/flexget/shared_invite/enQtNTQzNjM4MTY3ODYzLTA3NTRhZGNlMjBiN2FmNjZiZDVmZGQzMGFiODdhMWI1NjYyMzYwYWEyYjRlMGNjMWIzZTczMzMwZjdiODQ5OGI)
- [Discord](https://discord.gg/W6CQrJx)

## IRC
If you're considering IRC, you should look at Matrix as a modern alternative that captures its decentralized spirit while offering crucial upgrades. Unlike IRC, Matrix provides persistent message history across all your synced devices, built-in end-to-end encryption for superior security, and supports modern features like file sharing, replies, and video calls.
- [Libera.Chat](https://web.libera.chat/#flexget)

### Fixing annoying bot nicks
If you are connecting via IRC, it can get annoying when much of the chat is all done by the sync bot. There is a plugin for your IRC client to spoof the real nicknames for chat relayed by the bot.
- WeeChat
The [parse_relayed_msg.pl](https://weechat.org/scripts/source/parse_relayed_msg.pl.html/) script can pull usernames out of the message text from the relay bots and spoof them in nicklist (for auto complete) and the chat window.
- Other Clients
If something similar is possible with other clients, somebody add some docs here.