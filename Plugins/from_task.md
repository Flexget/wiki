# Task Input Plugin

This plugin runs another task, and inputs any accepted entries from that task
in this one. Any modifications made to the entries, or fields populated will
be preserved.

This is especially useful when you need to filter, or make modifications to
entries being provided to other plugins that accept inputs, e.g.
[discover](/Plugins/discover), or [configure_series](/Plugins/configure_series)

When another task is run via this plugin, the seen plugin will be disabled in
that task, unless it is explicitly configured there.

It may be useful to configure the [manual](/Plugins/manual) plugin on any task
you only want to be run by `from_task`. This will prevent that task from being
run on its own.

### Example
```yaml
tasks:
  useful-task:
    discover:
      what:
        - from_task: my-custom-searches
      from:
        - search_rss: http://somewhere
    # Do some other useful stuff here
  my-custom-searches:
    rss: http://someplace
    set:
      title: "{{title|replace('-', ' ')}}
    regexp:
      reject:
        - badthing
    accept_all: yes
    manual: yes
```
