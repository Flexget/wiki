---
title: Chat
description: 
published: true
date: 2025-08-27T14:00:59.291Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:48:47.761Z
---

# Chat
Connect with the community through various platforms. We utilize a bot to synchronize chats across all services, ensuring a seamless conversation regardless of your preferred client.

## Recommended Platforms

For an enhanced and user-friendly experience, we recommend joining our chat on one of these modern platforms. They offer persistent message history, file and image sharing, emoji reactions, and cross-device syncing. Thanks to our sync bot, conversations are bridged across all services, allowing you to choose the platform you're most comfortable with and still be part of the same discussion.

* Matrix protocol:
  * [Matrix](https://matrix.to/#/#flexget:matrix.org) (Matrix official server)
  * [Gitter](http://gitter.im/Flexget/Flexget) (Gitter is another Matrix server)
* [Slack](https://join.slack.com/t/flexget/shared_invite/enQtNTQzNjM4MTY3ODYzLTA3NTRhZGNlMjBiN2FmNjZiZDVmZGQzMGFiODdhMWI1NjYyMzYwYWEyYjRlMGNjMWIzZTczMzMwZjdiODQ5OGI)
* [Discord](https://discord.gg/W6CQrJx)

## IRC
If you're considering IRC, we encourage you to look at Matrix as a modern alternative. Matrix embodies the decentralized spirit of IRC while offering significant upgrades such as persistent message history, built-in end-to-end encryption, and support for modern features like file sharing and video calls.
* [Libera.Chat](https://web.libera.chat/#flexget)

### Improving the Experience on IRC: Fixing Annoying Bot Nicks
When connecting via IRC, you may find that messages from other platforms are relayed by a single sync bot, which can be visually disruptive. Some IRC clients can be configured with scripts to parse these relayed messages and display the original user's nickname, creating a more natural chat experience.
* **WeeChat**
The [parse_relayed_msg.pl](https://weechat.org/scripts/source/parse_relayed_msg.pl.html/) script can pull usernames out of the message text from the relay bots and spoof them in nicklist (for auto complete) and the chat window.
* **Other Clients**
    Achieving similar functionality in other IRC clients typically requires custom scripting. While no out-of-the-box solutions are as straightforward as the WeeChat script, most clients offer powerful scripting capabilities:
    *   **Irssi**: Known for its flexibility, Irssi can be extended with Perl scripts. You can find more information on how to get started with scripting in the official documentation and various online guides.
    *   **HexChat**: This client supports scripting in languages like Python and Lua. The official documentation provides a comprehensive guide to its plugin interface.
    *   **mIRC**: A long-standing Windows client with a powerful scripting language. Detailed documentation and community forums can help you create custom scripts to handle relayed messages.