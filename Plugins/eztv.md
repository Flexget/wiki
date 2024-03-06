# EZTV
Gets entries from the EZTV website

It's highly recommended to pair this with the [`limit` plugin](/Plugins/limit) otherwise it can take a long time to make the 15 calls to fetch 1500 entries

## As an Input
Will get the most recent entries from the website.


### Example
```yaml
my-task:
  limit:
    amount: 20
    what:
      - eztv: yes
```

## As a Search
It also works with the [`discover` plugin](/Plugins/discover), however your entries **must have** the `imdb_id` field since it's the only search allowed.

For example the simple form:

```yaml
my-task:
  limit:
    amount: 20
    from:
      discover:
        what: 
          - entry_list: my-series  # entries with imdb_id
        from:
          - eztv: yes
```