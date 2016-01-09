= Send Telegram =

Send a message to one or more Telegram users or groups upon accepting a download.


== Preparations ==

* Install 'python-telegram-bot' python pkg (i.e. `pip install python-telegram-bot`)
* Create a bot & obtain a token for it (see https://core.telegram.org/bots#botfather).
* For direct messages (not to a group), start a conversation with the bot and click "START" in the Telegram app.
* For group messages, add the bot to the desired group and send a start message to the bot: "/start" (mind the
  leading '/').


== Configuration example ==

{{{
my-task:
  send_telegram:
    bot_token: token
    template: {{title}}
    use_markdown: no
    recipients:
      - username: my-user-name
      - group: my-group-name
      - fullname:
          first: my-first-name
          sur: my-sur-name
}}}


== Bootstrapping and testing the bot ==

* Execute: `flexget send_telegram bootstrap`.
  Look at the console output and make sure that the operation was successful.
* Execute: `flexget send_telegram test-msg`.
  This will send a test message for every recipient you've configured.


== Configuration notes ==

You may use any combination of recipients types (`username`, `group` or `fullname`) - 0 or more of each (but you
need at least one total...).


== `template` ==
Optional. The template from the example is the default.

== `use_markdown` ==
Optional. Whether the template uses markdown formatting. The default is `no`.

NOTE: The markdown parser WILL crash if you have an unmatched amount of _ or * in your message (Underscores in URLs are especially tricky here)

== `username` vs. `fullname` ==

Not all Telegram users have a username. In such cases you would have to use the `fullname` approach. Otherwise, it
is much easier to use the `username` configuration.
