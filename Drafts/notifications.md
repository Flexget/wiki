= Notification plugins/phase
== Problem description

We currently have notifications plugins but they are limited to being a part of the `output` phase, which only outputs accepted entries. Having a way to get notified about other events, such as crashes, failed entries, errors and such would be highly beneficial.

== Proposed solution
* Create a `notification` phase.
* Modify current notifications plugins (like `telegram`, `pushbullet`, `email` and etc.) to support that phase. They will need the ability to be able to receive relevant event rather than just iterating over `task.accepted` as the currently do.
* Create events in various places in the code, like crash log dump, entry fail and etc.
* Define notifiers in a new root config node, `notifications`. There each relevant notifier plugin config will be set.
* Call the relevant notifier via its relevant event in task.

== Suggested config
```
notifiers:
  pushbullet:
    api_key: token
  telegram:
    token: token
  email: {opts}

tasks:
  series_task:
    rss: "http://url.com/link/"
    series:
      - series name
    download: /path/to/downloads
    notify:
      on_error:
        - pushbullet
      on_crash:
        email:
          message: OMG, A CRASH! # All plugin attributes should be accessible to override defaults. 
      on_fail:
        - internal # A new internal plugin that would be accessible via API/CLI/output to log (???)
```
== Potential issues
* Many hooked event can cause notification flooding, we need an internal way to take care of that and make it configurable