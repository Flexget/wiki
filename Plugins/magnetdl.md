# Magnetdl

Works as input or as a search plugin.

## Configuration

| Option | Default | Description |
| --- | --- | --- |
| category | tv | One of 'software', 'movies', 'games', 'e-books', 'tv', 'music' |
| pages | 5 | How many pages to retrieve

There's intelligent caching to avoid retrieving pages which have already been processed.

## Examples

```yaml
magnetdl:
  category: tv
```