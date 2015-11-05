= Send Telegram =

Send a message to one or more Telegram users or groups upon accepting a download.


== Preparations ==

* Install 'python-telegram-bot' python pkg
* Create a bot & obtain a token for it (see https://core.telegram.org/bots#botfather).
* For direct messages (not to a group), start a conversation with the bot and click "START" in the Telegram app.
* For group messages, add the bot to the desired group and send a start message to the bot: "/start" (mind the
  leading '/').


== Configuration example ==

{{{
my-task:
  send_telegram:
    bot_token: token
      recipients:
        - username: my-user-name
        - group: my-group-name
        - fullname:
            first: my-first-name
            sur: my-sur-name
}}}

You may use any combination of recipients types (`username`, `group` or `fullname`) - 0 or more of each (but you
need at least one total...).


== `username` vs. `fullname` ==

Not all Telegram users have a username. In such cases you would have to use the `fullname` approach. Otherwise, it
is much easier to use the `username` configuration.
