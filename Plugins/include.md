= Include =

Allows including configuration from another file into a feed.

=== Example ===


'''config.yml'''

{{{
feeds:
  stuff:
    include: series.yml
    download: ~/downloads/
}}}

'''series.yml'''

{{{
series:
  - foo
  - bar
}}}

This allows parts of configuration to be shared between multiple configuration files.