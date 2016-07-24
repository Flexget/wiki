# Tail
Similar to the [text](/Plugins/text) plugin but remembers the file position and continues from it. This plugins does NOT work for log files that are rotated.

**Example:**

```
tail:
  file: ~/irclogs/some/log
  entry:
    title: 'TITLE: (.*) URL:'
    url: 'URL: (.*)'
  encoding: utf8
```

The default encoding will be utf8 if none has been specified in the config. If you are getting `?` instead of non-ascii characters in your entries, you have likely specified the wrong encoding.

If the log file is detected to be smaller than in previous scan the position is reseted.

To reset file position manually use `--tail-reset FILE`