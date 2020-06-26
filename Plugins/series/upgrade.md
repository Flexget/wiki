# Upgrade
Upgrade mode causes the series plugin to continue accepting the better quality of an episode than what have been previously accepted. It also blocks acepting any episodes that are of a worse quality than what already has been accepted. 

It can optionally be used alongside the [qualities](/Plugins/series/qualities) option or [quality](/Plugins/series/quality) options to restrict which qualities will be upgraded to. Please refer to previously mentioned options for additional information.

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
