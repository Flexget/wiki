# Accept all
Really simple plugin, just accepts all entries. Remember that accepted entries can still be rejected by other plugins.

### Example

```yaml
tasks:
  prefiltered_feed:
    rss: http://example.com/filtered.rss
    accept_all: yes
```

This will accept everything from the defined feed. NOTE: you need an [output plugin](/Plugins#Outputs) defined to actually download something.