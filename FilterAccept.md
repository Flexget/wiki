# Accept

Entries matching regexp will be accepted.
Non matching entries are not intervened.

Example:

```
imdb:
  min_score: 6.4
accept:
  - rush.hour.3
```

Now rush hour 3 will be passed even if imdb filter would cause it
to be filtered because of min_score.

See module [patterns](/FilterPatterns) documentation for full syntax.
Unconditionally supports `not` and `path` directives like [patterns](/FilterPatterns).