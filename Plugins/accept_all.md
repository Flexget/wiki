= Accept all =

Really simple plugin, just accepts all entries. Remember that accepted entries can still be rejected by other plugins.

'''Example:'''

{{{
tasks:
  prefiltered_feed:
    rss: http://example.com/filtered.rss
    accept_all: yes
}}}

This will accept everything from the defined feed. NOTE: you need an [wiki:Plugins#Outputs output plugin] defined to actually download something.