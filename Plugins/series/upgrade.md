# Upgrade
Upgrade mode causes the series plugin to continue getting the best quality of an episode it sees. It also blocks any episodes that are of a worse quality than you already have. It can be used alongside the [qualities](/Plugins/series/qualities) option or [quality](/Plugins/series/quality) options to restrict which qualities will be upgraded to.

### Example
```yaml
series:
  - name of the series:
      upgrade: yes
      qualities:
        - hdtv
        - hdtv 720p
        - bluray 1080p
```

### Example

```yaml
series:
  - name of the series:
      upgrade: yes
      quality: hdtv-bluray 720p-1080p 
```
