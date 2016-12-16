# Chat
Chat can be accessed via multiple ways. We are using a bot to sync chat between Gitter, and #flexget in freenode IRC.

## Gitter Web Client
[Gitter](http://gitter.im/Flexget/Flexget) has a rich web interface, accessible anywhere, with backlog built in. If you are not already using IRC for anything else, this is probably the nicest chatting method.

## IRC
There are a couple of ways to chat via IRC client now.

### #flexget on Freenode
You can still chat on our channel on the freenode IRC network. All chat from gitter is relayed to the channel via a bot (`FGitterBot`.)

### #Flexget/Flexget on irc.gitter.im
Gitter runs its own IRC bridge, which allows you to log in to gitter via IRC. Here, all messages from freenode will be relayed via a bot (`FlexGet-Bot`.) Go [here](http://irc.gitter.im) for instructions on how to connect to the Gitter IRC bridge.

### Fixing annoying bot nicks
If you are connecting via IRC, it can get annoying when much of the chat is all done by the sync bot. You can mitigate this choosing to connect to the irc server where most of the chat is coming from. If you are more tenacious, there may be a plugin for your IRC client to spoof the real nicknames for chat relayed by the bot.

**WeeChat**
The [parse_relayed_msg.pl](https://weechat.org/scripts/source/parse_relayed_msg.pl.html/) script can pull usernames out of the message text from the relay bots and spoof them in nicklist (for auto complete) and the chat window.

**Other Clients**
If something similar is possible with other clients, somebody add some docs here.