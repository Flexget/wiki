# Accept all

Accepts all entries in the task. Remember that accepted entries can still be rejected by other plugins.

### Example

```yaml
tasks:
  prefiltered_feed:
    rss: http://example.com/filtered.rss
    accept_all: yes
```

This will accept everything from the defined feed. 

**NOTE:** You will need an [output plugin](/Plugins#Outputs) configured to actually do something with accepted entries (eg. download).