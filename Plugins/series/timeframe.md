---
title: timeframe
description: 
published: true
date: 2025-02-21T04:53:36.004Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:28:38.635Z
---

# Timeframe and Target
Timeframe value: NUM (minutes|hours|days|weeks)

Specify a timeframe in which FlexGet waits for the chosen quality. The desired quality should be given with `target` option, and should be a valid [quality requirements](/Qualities#Requirements) string. If specified quality does not become available within given timeframe after a different quality has been seen, best quality so far is chosen. `target` has default value of 720p hdtv+ when timeframe option is given. 

**IMPORTANT NOTE**: If you also specify the [quality](/Plugins/series/quality) option along with timeframe, it will be enforced no matter what (both before and after the timeframe expires.) "enforced" doesn't mean that quality will be picked, it just means things that don't match it will be ignored.

**Example:**

Wait for 720p hdtv release for 4 hours, if not available in that timeframe accept best episode seen, can be lower OR higher in quality.

```yaml
series:
  - some series:
      timeframe: 4 hours
      target: 720p hdtv
  - another series
  - third series
```

**Example:**

Wait for 12 hours for 1080p webdl and after that fall back to anything between 720p-1080p in resolution from webdl source.

```yaml
series:
  - some series:
      timeframe: 12 hours
      target: 1080p webdl
      quality: 720p-1080p webdl
```

**Example:**

Wait for 2 hours for 1080p, and if not found after the 2 hours, download anything higher quality than 1080p. This is useful for example to wait some time for a lower quality, and grab a higher one if the lower quality doesn't appear. Think of it like [upgrade](/Plugins/series/upgrade) without two quality downloads.

```yaml
series:
  - some series:
      timeframe: 2 hours
      target: 1080p
      quality: 1080p+
```

### Behavior with qualities option
If the [qualities](/Plugins/series/quality) option is defined alongside timeframe (instead of `target`), the timeframe will only kick in if *none* of your defined qualities have been downloaded within the timeframe.

### Behavior with upgrade option
If the [upgrade](/Plugins/series/upgrade) option is defined along with `target`, the target quality will still be allowed to download if it becomes available after a fallback quality has already been accepted. **Note**: It will not allow upgrades that are worse than the target quality.

Note that [upgrade](/Plugins/series/upgrade) will not upgrade once the `target` quality has been reached even if the target is a range.

### Force Timeframe to Stop
If you'd like the series plugin to stop waiting for your target quality, and accept whatever the current best episode is, you can run the task with the `--stop-waiting` flag. You'll need to specify the name of the series you'd like as well, e.g. `flexget execute --stop-waiting "pioneer one"`.