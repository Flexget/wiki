# Tracking
Series plugin keeps track of downloaded episodes for each series and rejects episodes that are too far in the past or future from the latest downloaded one. Past seasons are not be allowed, and only the first couple eps in the next season are allowed. This helps prevent skipping back to old seasons, or skipping too far ahead and missing episodes.

**Example:**
Pioneer One latest episode is S02E22 and suddenly a feed contains S01E01 which series plugin has not seen or downloaded.  
**Result:**
Episode advancement rejects this episode since it's too far in the past.

**Example:**
 Pioneer One latest episode is S02E22 and suddenly a feed contains S02E20 which series plugin has not seen or downloaded.  
**Result:**
Episode advancement does not reject this. Old eps from current season are allowed.

## Resolutions

There are many ways to address this issue.

### Set starting point via CLI

You can set starting point easily via commandline. 

**Example:**

```bash
$ flexget series begin "Pioneer One" S03E01
```

### Config Options
If you would like to disable this behavior for some or all series, and allow getting episodes in any order, you can set this option to `no` in the series plugin config.

```yaml
tracking: no
```

If you want to prevent skipping forward too far, but allow any previous seasons to be downloaded, you can put tracking in to `backfill` mode:

```yaml
tracking: backfill
```

### Disabling during execution from CLI
Tracking can sometimes be problematic if you have huge gap of recent episodes in `series` database. You can temporarily disable this feature by executing the task with the `--disable-tracking` flag allowing FlexGet to grab latest episode and continue properly from there.

**Example:**

```bash
$ flexget execute --disable-tracking
```

```bash
$ flexget inject --disable-tracking
```
