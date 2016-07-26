# Sceper
Uses sceper.ws category url as input.

**`NOTE:`** This plugin relies on urlrewriters to rewrite to a valid download link. Certain urlrewriters may need to be disabled on the task if they do not produce the download links, most notably `urlrewrite_redirect`.

#### Example:

```yaml
tasks:
  some-task:
    sceper: http://sceper.ws/category/tv-shows/tv-shows-x264
    disable_urlrewriters: [urlrewrite_redirect]
```