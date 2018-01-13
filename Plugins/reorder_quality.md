# Reorder Quality

This plugin allows you to reorder the built-in [qualities](../Qualities) in a simple fashion. Qualities can only be reordered within the same quality component eg. you cannot make a codec be above a resolution.

### Config
```text
  reorder_quality:
    <name>:
      above|below: <another name>
```

### Example
This example will prefer webrip over hdtv.
```yaml
  download-task:
    rss: ...
    series:
      - WebRipRules
    reorder_quality:
      webrip:
        above: hdtv
```